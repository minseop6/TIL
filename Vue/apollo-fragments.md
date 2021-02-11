# Vue Apollo Fragments
- `query`에 사용될 필드들을 재사용 할 수 있도록 해줌

```js
// user-info.fragment.gql
fragment UserInfo on User {
    firstName
    lastName
    age
    gender
}
```

```js
// get-user.query.gql
#import './user-info.fragmet.gql'

query getUser($userId: Int!) {
    getUser(userId: $userId) {
        ...UserInfo
        friends {
            ...UserInfo
        }
    }
}
```