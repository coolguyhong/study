## Vuex

### Vuex

- Vue.js 애플리케이션에 대한 상태 관리 패턴 + 라이브러리 입니다. 애플리케이션의 모든 컴포넌트에 대한 중앙 집중식 저장소 역할을 하며 예측 가능한 방식으로 상태를 변경할 수 있습니다.

### 일반적인 Flow

![일반적인 flow](https://vuex.vuejs.org/kr/images/flow.png)

- State: Data in Vue Component
- View: State에 따른 Vue Template
- Action: View에서 State에 영향을 주는 행위(ex: event, etc)
- 공통의 State를 공유해야 하는 컴포넌트가 여럿 있으면 복잡한 Props의 관계가 생겨난다.

### Vuex flow

![vuex flow](https://vuex.vuejs.org/kr/images/vuex.png)

- State: 상동
    + DB
- Mutations: State를 바꿀 수 있는 유일한 객체, State를 바꾸는 단위 동작
    + DAO
- Actions: Mutations으로 처리하기 애매한 동작(비동기 호출에 의한 State 변경)
    + Service
- Vue Components: 사용자의 조작 등을 통한 Actions 발생

### Vuex를 언제 사용해야 하는가?

- 공유된 상태 관리 처리엔 유용
- 하지만, 개념에 대한 이해와 시작하는 비용이 큼
- 중대형 SPA를 구축하는 경우에 고려하면 좋음
- Flux 라이브러리는 안경과 같습니다. 필요할 때 알아볼 수 있습니다.

### Store

- State를 보유하고 Readonly로 공개
- Actions을 발행할 수 있는 Dispatch 메소드를 공개

#### Store의 State의 변경에 대응하는 방법

 Vue Component의 Computed를 이용하여 변경을 감지

 ```javascript
 const Counter = {
   template: `{{ count }}`,
   computed: {
     count () {
       return this.$store.state.count
     }
   }
 }
 ```

 #### 주의해야 하는 점

 - Vuex를 사용한다고 해서 Vuex에 모든 상태를 넣어야 하는 것은 아님
 - 코드를 보다 장황하고 간접적으로 만들 수도 있음
- State가 단일 컴포넌트에만 영향을 주는 경우 로컬 상태가 유리

### Getters

- Store의 computed

```javascript

const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})
```

- 다른 getters를 통해 정의할 수도 있음

```javascript

getters: {
  // ...
  doneTodosCount: (state, getters) => {
    return getters.doneTodos.length
  }
}
store.getters.doneTodosCount // -> 1
```

### Mutations

- 실제로 State를 바꿀 수 있는 유일한 방법
- 이벤트와 매우 유사
- 각 Mutation은 직접 호출할 수 없고 store.commit을 거쳐야 함

```javascript
// ...
mutations: {
  increment (state, n) {
    state.count += n
  }
}
store.commit('increment', 10)
```

#### State 변경시 주의사항

- Mutation은 무조건 동기적으로 수행되어야 함
    + Mutation 함수는 동기적으로 작성되어야만 함
    + Mutation 수행 "이전" 및 "이후" 를 스냅샷하여 사용하기 때문에, 비동기적 State 변경은 추적되어지지 않음
- Vuex 저장소의 State 변경은 상태를 관찰하는 Vue 컴포넌트에 자동으로 업데이트되므로 주의사항이 존재
    + 사용할 모든 State의 Field는 초기화 이후 사용하는 것이 좋음
    + State 하위에 새로운 객체를 추가할때는 Vue\.set을 사용하거나, 객체를 새로운 것으로 교체하는 두가지 방법중 하나를 사용해야만 함

```javascript
Vue.set(obj, 'newProp', 123)
// or
state.obj = { ...state.obj, newProp: 123 }
```


### Actions

- 직접적으로 State를 변경하지 않고, Commit을 통해 State를 변경하므로 비동기적 작업이 필요할때 사용할 수 있음
- Action은 dispatch 메소드 호출을 통해 수행되며, Payload를 함께 전달 가능

```javascript
const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment (state, n) {
      state.count += n
    }
  },
  actions: {
    increment (context, n) {
      context.commit('increment', n)
    }
  }
})
store.dispatch('increment', 10)
```

#### Actions 수행이 비동기적으로 수행될 때

- Action의 반환값으로 Promise를 전달
```javascript
actions: {
  actionA ({ commit }) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        commit('someMutation')
        resolve()
      }, 1000)
    })
  }
}
store.dispatch('actionA').then(() => {
 // ...
})
```

- 액션 안에 또 다른 액션 사용도 가능
```javaScript
actions: {
  // ...
  actionB ({ dispatch, commit }) {
    return dispatch('actionA').then(() => {
      commit('someOtherMutation')
    })
  }
}
```

- ES6의 async/await도 이용 가능
```javaScript
// getData() 및 getOtherData()가 Promise를 반환한다고 가정합니다.
actions: {
  async actionA ({ commit }) {
    commit('gotData', await getData())
  },
  async actionB ({ dispatch, commit }) {
    await dispatch('actionA') // actionA가 끝나기를 기다립니다.
    commit('gotOtherData', await getOtherData())
  }
}
```

### Modules

- 단일 상태 트리를 사용하기 때문에 모든 State가 한 객체에 표현
- 때문에 규모가 커짐에 따라 저장소가 비대해짐
- 이럴 때 Vuex는 Module을 이용하도록 권장
    + [한글 모듈 문서](https://vuex.vuejs.org/kr/modules.html)
    + [영문 모듈 문서](https://vuex.vuejs.org/en/modules.html)
