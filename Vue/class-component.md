# Class Component

- `@Component` decorator 사용하면 클래스 컴포넌트 사용 가능
```js
import Vue from 'vue'
import Component from 'vue-class-component'

@Component
export default class ExampleClass extends Vue { }
```

- `data`는 클래스의 `property`로 선언 가능
```js
<template>
  <div>{{ exampleData }}</div>
</template>

<script lang="ts">
import Vue from 'vue'
import Component from 'vue-class-component'
@Component
export default class ExampleClass extends Vue {
    private exampleData: string = 'example';
}
</script>
```

- `method`는 클래스의 `function`으로 선언 가능
```js
@Component
export default class ExampleClass extends Vue {
    private exampleMethod(): string {
        return 'Example Method';
    }
}
```

- `Computed property`는 클래스의 `getter/setter`로 선언 가능
```js
@Component
export default class ExampleClass extends Vue {
    private name: string = "Example";

    get name() {
        return this.name;
    }

    set name(name: string) {
        this.name = name;
    }
}
```