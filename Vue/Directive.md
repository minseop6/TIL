# Directive

- `Vue`에서 제공하는 특수 속성으로 `v-` 접두어가 붙어있음
- 렌더링 된 `DOM`에 특수한 반응형 동작을 지시

## 종류

1. ### v-text

- `{{ }}`의 기능과 동일

```js
<template>
  <div>
    <div v-html="message"></div>
  </div>
</template>

<script>
import Vue from "vue";
export default class About extends Vue {
  message = "Hello Vue!!";
}
</script>
```

2. ### v-html

- `HTML` 태그를 지원

```js
<template>
  <div>
    <div v-html="message"></div>
  </div>
</template>

<script>
import Vue from "vue";
export default class About extends Vue {
  message = "<i>Hello Vue!!<i>";
}
</script>
```

3. ### v-show

- 해당 엘리먼트를 보여줄지 여부(true/false)

```js
<template>
  <div>
    <div v-show="visible">
      <span v-text="message"></span>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
export default class About extends Vue {
  visible = true;
  message = "Hello Vue!!";
}
</script>
```

4. ### v-if

- 엘리먼트의 표시 여부에 대한 조건문
- `v-else-if`, `v-else`

```js
<template>
  <div>
    <div>
      <span v-if="value > 5">value > 5</span>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
export default class About extends Vue {
  value = 11;
}
</script>

<style></style>
```

5. ### v-pre

- 해당 엘리먼트에 지시문이 없다는걸 컴파일러에게 알려 컴파일 타임에 건너뜀
- 컴파일 속도를 향상 시킬 수 있음

6. ### v-cloak

- `Vue` 인스턴스가 준비되기 전 템플릿을 위한 `HTML`코드를 숨길 때 사용

```js
<template>
  <div>
    <div v-cloak>
      <span v-if="value > 5">value > 5</span>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
export default class About extends Vue {
  value = 11;
}
</script>

<style>
[v-cloak] {
  display: none;
}
</style>

```

7. ### v-for

```js
<template>
  <div>
    <div>
      <ol>
        <li v-for="todo in todos" v-bind:key="todo.id">{{ todo.text }}</li>
      </ol>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
export default class About extends Vue {
  todos = [
    {
      id: 1,
      text: "todo1"
    },
    {
      id: 2,
      text: "todo2"
    },
    {
      id: 3,
      text: "todo3"
    }
  ];
}
</script>
```

8. ### v-on

- 사용자와 애플리케이션이 상호 작용할 수 있도록 메소드를 호출하는 이벤트 리스너 추가

```js
<template>
  <div>
    <div>
      <div>{{ message }}</div>
      <button v-on:click="reverseMessage">Message Reverse</button>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import Component from "vue-class-component";

@Component
export default class About extends Vue {
  message = "Hello Vue!";

  reverseMessage() {
    this.message = this.message
      .split("")
      .reverse()
      .join("");
  }
}
</script>
```

9. ### v-model

- 입력에 대한 애플리케이션 상태를 양방향으로 바인딩

```js
<template>
  <div>
    <div>
      <div>{{ message }}</div>
      <input type="text" v-model="message" />
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import Component from "vue-class-component";

@Component
export default class About extends Vue {
  message = "Hello Vue!";
}
</script>
```

10. ### v-bind

- `HTML` 엘리먼트 속성에 데이터 값을 사용할 때 사용
- `v-bind`를 생략하고 콜론과 속성 이름만으로도 적용 가능

```js
<template>
  <div>
    <div>
      <img v-bind:src="img" />
      <img :src="img" />
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import Component from "vue-class-component";

@Component
export default class About extends Vue {
  img = "http://test.com/example.jpg";
}
</script>
```
