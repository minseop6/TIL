# 전역 API

## Vue.extends(options)
- 전달인자
    - `{Object} options`
- 사용방법
    - Vue 생성자의 하위 클래스를 만듦
    - 전달인자는 옵션을 포함하는 객체

## Vue.nextTick([callback, context])
- 전달인자
    - `{Function} [callback]`
    - `{Object} [context]`
- 사용방법
    - 다음 DOM 업데이트 사이클 이후 실행하는 콜백을 지연시킴
    - DOM 업데이트를 기다리기 위해 일부 데이터를 변경한 직후 사용해야함

```js
this.$nextTick(() => {
    console.log('next tick');
})

this.$nextTick().then(() => {
    console.log('usage as a promise');
})
```

## Vue.set(target, propertyName/index, value)
- 전달인자
    - `{Object | Array} target`
    - `{string | number} propertyName/index`
    - `{any} valye`
- 반환 값: 설정한 값
- 사용방법
    - 객체에 대한 속성을 설정
    - 객체가 반응형이면, 속성이 반응형 속성으로 만들어지고 뷰 업데이트를 방생시킴
    - Vue가 객체 속성 추가를 감지하지 못하는 문제점을 해결할 수 있음

## Vue.delete(target, propertyName/index)
- 전달인자
    - `{Object | Array} target`
    - `{string | number} propertyName/index`
- 사용방법
    - 객체의 속성을 삭제
    - 객체가 반응형이면, 뷰 업데이트를 발생시킴
    - Vue가 객체 속성 삭제를 감지하지 못하는 문제점을 해결할 수 있지만 사용을 지양해야함

## Vue.directive(id, [definition])
- 전달인자
    - `{string} id`
    - `{Function | Object} [definition]`
- 사용방법
    - 전역 디렉티브를 등록하거나 검색
    - [(참고)사용자 지정 디렉티브](https://kr.vuejs.org/v2/guide/custom-directive.html)

## Vue.filter(id, [definition])
- 전달인자
    - `{string} id`
    - `{Function} [definition]`
- 사용방법
    - 전역 필터를 등록하거나 검색
    
```js
// 등록
Vue.filter('sum', (a, b) => {
    return a, b;
})

// getter, 필터가 등록된 경우 반환
const testFilter = Vue.filter('sum');
```

## Vue.component(id, [definition])
- 전달인자
    - `{string} id`
    - `{Function | Object} [definition]`
- 사용방법
    - 전역 컴포넌트를 등록하거나 검색
    - 등록 시 자동으로 컴포넌트의 `name`을 주어진 `id`로 설정

## Vue.use(plugin)
- 전달인자
    - `{Object | Function} plugin`
- 사용방법
    - Vue.js 플러그인을 설치
    - 플러그인이 Object인 경우 `install` 메소드를 사용해야함

## Vue.mixin(mixin)
- 전달인자
    - `{Object} mixin`
- 사용방법
    - 전역으로 mixin을 적용
    - 생성된 모든 Vue 인스턴스에 여향을 줌
    - 플러그인 작성자가 컴포넌트에 사용자 정의 동작을 주입하는데 플러그인을 사용할 수 있음
    - 어플리케이션 코드에서는 사용을 지양해야함

## Vue.compile(template)
- 전달인자
    - `{string} template`
- 사용방법
    - 템플릿 문자열을 렌더링 함수로 컴파일함
    - 전체 빌드에서만 가능
    
```js
const res = Vue.compile('<div><span>{{ msg }}</span></div>')

new Vue({
  data: {
    msg: 'hello'
  },
  render: res.render,
  staticRenderFns: res.staticRenderFns
})
```

## Vue.observable(object)
- 전달인자
    - `{Object} object`
- 사용방법
    - 객체를 반응형으로 만들어줌
    - 내부적으로 Vue는 데이터 함수에 의해 반환된 객체를 사용
    - 반환된 객체는 `render function`과 `computed properties`내에서 직접 사용 가능
    - 수정될 때 적절한 업데이트를 실행시킴

```js
const state = Vue.observable({ count: 0 })

const Demo = {
  render(h) {
    return h('button', {
      on: { click: () => { state.count++ }}
    }, `count is: ${state.count}`)
  }
}
```


## Vue.version
- 설치된 Vue 버전을 가져올 수 있음