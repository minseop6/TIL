# 접근자 프로퍼티(Accessor Property)
- 객체가 가진 프로퍼티 값을 외부에서 직접 접근안하고 사용할 수 있게해주는 메소드

## getter

```js
class User {
    private firstName: "Gildong";
    private lastName: "Hong";

    get fullName() {
        return `${this.firstName} ${this.lastName}`
    }
}

```

```js
const user = new User();

console.log(user.fullName); // Gildong Hong
```

## setter

```js
class User {
    private firstName: "Gildong";
    private lastName: "Hong";

    set fullName(fullName) {
        [this.firstName, this.lastName] = fullName.split(" ");
    }
}
```

```js
const user = new User();

user.fullName = "Minseop Kim";
```