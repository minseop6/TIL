# Vue Life Cycle

<img src="../img/Vue/vue-lifecycle.png" width="600" height="1000">

## beforeCreate
- Vue 인스턴스가 초기화 된 직후에 실행
- 컴포넌트가 DOM에 추가되기 전이어서 `this.$el`에 접근할 수 없음
- 데이터와 메소드도 접근할 수 없음

## created
- 컴포넌트가 DOM에 추가되기 전이어서 `this.$el`에 접근할 수 없음
- 데이터와 메소드에 접근 가능
- 이벤트 리스너 선언을 하기에 적합

## beforeMount
- 템플릿의 여부를 확인한 후 렌더링하여 가상 DOM이 생성됨
- 가상 DOM이 실제 DOM에 부착되진 않음

## mounted
- 가상 DOM이 실제 DOM에 부착되고 난 후에 실행됨
- `this.$el`에 접근할 수 있음
- 자식 컴포넌트가 mount된 이후에 부모 컴포넌트가 mount됨

## beforeUpdate
- 컴포넌트에서 사용되는 데이터의 값이 변해서 DOM에 변경사항을 적용시키기 전에 실행됨
- `beforeUpdate`훅에서 값을 변경해도 렌더링을 추가 호출하지 않음

## updated
- 가상 DOM을 렌더링하고 실제 DOM이 변경된 이후에 실행됨
- `updated` 훅에서 데이터를 변경하면 무한 루프가 발생할 수 있으므로 `this.$nextTick`을 이용해 DOM이 렌더링 된 이후의 상태를 변경

## beforeDestroy
- 인스턴스가 해제되기 전에 실행됨
- 아직 인스턴스가 살아있는 상태이므로 모든 데이터와 메소드에 접근 가능
- 이벤트 리스너 해제 등 인스턴스가 해제되기 전에 해야할 작업에 적합

## destroyed
- 인스턴스가 해제된 직후에 실행됨
- 모든 데이터와 메소드에 접근할 수 없음