## Spring Exception

### Controller Based Exception Handling

- @ExceptionHandler 사용
- Controller 단위로 처리하며, 필요한 Controller 내부에 작성
- Controller 수행중 @ExceptionHandler에 함께 작성된 Exception이 발생할 경우, 해당 메소드가 수행
```Java
@Controller
public class ExceptionHandlingController {

  // @RequestHandler methods
  ...

  // Exception handling methods

  // Convert a predefined exception to an HTTP Status code
  @ResponseStatus(value=HttpStatus.CONFLICT,
                  reason="Data integrity violation")  // 409
  @ExceptionHandler(DataIntegrityViolationException.class)
  public void conflict() {
    // Nothing to do
  }

  // Specify name of a specific view that will be used to display the error:
  @ExceptionHandler({SQLException.class,DataAccessException.class})
  public String databaseError() {
    // Nothing to do.  Returns the logical view name of an error page, passed
    // to the view-resolver(s) in usual way.
    // Note that the exception is NOT available to this view (it is not added
    // to the model) but see "Extending ExceptionHandlerExceptionResolver"
    // below.
    return "databaseError";
  }

  // Total control - setup a model and return the view name yourself. Or
  // consider subclassing ExceptionHandlerExceptionResolver (see below).
  @ExceptionHandler(Exception.class)
  public ModelAndView handleError(HttpServletRequest req, Exception ex) {
      logger.error("Request: " + req.getRequestURL() + " raised " + ex);

      ModelAndView mav = new ModelAndView();
      mav.addObject("exception", ex);
      mav.addObject("url", req.getRequestURL());
      mav.setViewName("error");
      return mav;
    }
}
```

### Global Exception Handling

- @ ControllerAdvice 사용
- 개별 Controller 가 아닌 전체 Controller에 대해 동작
- 메소드에 @ExceptionHandler 사용
```java
@ControllerAdvice
class GlobalDefaultExceptionHandler {
  public static final String DEFAULT_ERROR_VIEW = "error";

  @ResponseStatus(HttpStatus.CONFLICT)  // 409
  @ExceptionHandler(DataIntegrityViolationException.class)
  public void handleConflict() {
        // Nothing to do
  }

  @ExceptionHandler(value = Exception.class)
  public ModelAndView
  defaultErrorHandler(HttpServletRequest req, Exception e) throws Exception {
      // If the exception is annotated with @ResponseStatus rethrow it and let
      // the framework handle it - like the OrderNotFoundException example
      // at the start of this post.
      // AnnotationUtils is a Spring Framework utility class.
      if (AnnotationUtils.findAnnotation
                  (e.getClass(), ResponseStatus.class) != null)
        throw e;

      // Otherwise setup and send the user to a default error-view.
      ModelAndView mav = new ModelAndView();
      mav.addObject("exception", e);
      mav.addObject("url", req.getRequestURL());
      mav.setViewName(DEFAULT_ERROR_VIEW);
      return mav;
    }
}
```

### HandlerExceptionResolver

- Spring이 default로 등록해주는 ExceptionResolver
- ExceptionHandlerExceptionResolver: 발생한 예외들을 @ExceptionHandler 에 의해 지정된 메소드와 연결시켜주는 처리를 수행
- ResponseStatusExceptionResolver: 발생한 예외들을 @ResponseStatus 가 선언된 메소드 또는 클래스와 연결
- DefaultHandlerExceptionResolver: Spring Standard Exception 들을 HTTP Status Code 로 변환해주는 역할을 수행

### SimpleMappingExceptionResolver

- Exception 과 View를 연결시킬 수 있는 설정을 제공
- 기본 에러페이지 설정을 제공
- 로그메시지 활성화 가능
```Java
@Configuration
@EnableWebMvc  // Optionally setup Spring MVC defaults (if you aren't using
               // Spring Boot & haven't specified @EnableWebMvc elsewhere)
public class MvcConfiguration extends WebMvcConfigurerAdapter {
    @Bean(name="simpleMappingExceptionResolver")
    public SimpleMappingExceptionResolver
                    createSimpleMappingExceptionResolver() {
      SimpleMappingExceptionResolver r =
                  new SimpleMappingExceptionResolver();

      Properties mappings = new Properties();
      mappings.setProperty("DatabaseException", "databaseError");
      mappings.setProperty("InvalidCreditCardException", "creditCardError");

      r.setExceptionMappings(mappings);  // None by default
      r.setDefaultErrorView("error");    // No default
      r.setExceptionAttribute("ex");     // Default is "exception"
      r.setWarnLogCategory("example.MvcLogger");     // No default
      return r;
    }
    ...
}
```
