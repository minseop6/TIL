# Mixin
- `Vue` 컴포넌트에 재사용 가능한 기능을 사용할 수 있게 해주는 유연한 방법
- `mixin` 객체는 모든 컴포넌트 옵션을 포함할 수 있음
- 컴포넌트에서 `mixin`을 사용하면 `mixin`의 모든 옵셜들은 컴포넌트 고유 옵션에 혼합됨

```js
@Component
class TestMixin extends Vue {
    private name: string = 'Test Mixin'
    
    private mounted(): void {
        console.log(`${this.name}`);
    }
}

@Component({
    mixins: [TestMixin]
})
export default class TestComponent extends Vue {
    private mounted(): void {
        console.log('Test Component');
    }
}

// -Result-
// Test Mixin
// Test Component
```

## Option Merging
- `mixin`과 컴포넌트에 중복된 옵션이 있으면 적절한 적략을 사용해 병합됨
- 훅 함수는 동일한 이름은 배열로 병합되어 모두 호출되고 `mixin` 훅이 컴포넌트 후보다 먼저 호출됨 

```js
@Component
class TestMixin extends Vue {
    private name: string = 'Test Mixin';
    private message: string = 'Test Message';

    private mounted(): void {
        console.log(this.name, this.message);
    }
}

@Component({
    mixins: [TestMixin]
})
export default class TestComponent extends Vue {
    private name: string = 'Test Component';

    private mounted(): void {
        console.log(this.name, this.message);
    }
}

// -Result-
// Test Mixin Test Message
// Test Component Test Message
```