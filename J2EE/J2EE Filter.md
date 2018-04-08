## J2EE Filter

### 개요

- 서블릿으로 요청되는 Request 또는 Response 의 filtering 작업을 수행하기 위해 정의된 스펙
![J2EE Filter](https://greannetwork.files.wordpress.com/2012/08/presentation1.png)

### Java Interface

- Servlet Container 에 의해 사용되어지는 Interface
- void init(FilterConfig filterConfig: Filter 생성시 호출되는 Hook
- void destroy(): Filter 종료시 호출되어 지는 Hook
- doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
    + filterChain.doFilter(...) 를 호출하여 다음 등록된 Filter를 수행하며, 마지막 필터 이후에는 대상 Servlet 이 호출
    ```Java
    public class MyFilter implements Filter {

        FilterConfig filterConfig = null;

        public void init(FilterConfig filterConfig) throws ServletException {
            this.filterConfig = filterConfig;
        }

        public void destroy() {
        }

        public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain)
                throws IOException, ServletException {
            // Servlet 이 호출되기 전 수해할 작업
            filterChain.doFilter(servletRequest, servletResponse);
            // Servlet 이 호출된 후 수행할 작업
        }
    }
    ```

### J2EE FIlter 예시

- Authentication Filters
- Logging and Auditing Filters
- Image conversion Filters
- Data compression Filters
- Encryption Filters
- Tokenizing Filters
- Filters that trigger resource access events
- XSL/T filters
- Mime-type chain Filter

### 필터 설정
```xml
<web-app>

   <filter>
      <filter-name>HighlightFilter</filter-name>
      <filter-class>javacan.filter.HighlightFilter</filter-class>
      <init-param>
         <param-name>paramName</param-name>
         <param-value>value</param-value>
      </init-param>
   </filter>

   <filter-mapping>
      <filter-name>HighlightFilter</filter-name>
      <url-pattern>*.txt</url-pattern>
   </filter-mapping>

</web-app>
```
