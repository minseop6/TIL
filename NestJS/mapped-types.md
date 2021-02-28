# Mapped types
- 엔티티 필드들을 변형할 때 유용

## Installation
```powershell
$ npm i --save @nestjs/mapped-types
```

## Mapped types
- `PartialType` : 모든 필드들을 `optional`로 구성
- `PickType` : 선택된 필드들을 구성
- `OmitType` : 선택된 필드들을 제외한 나머지 필드들로 구성
- `IntersectionType` : 두 타입을 하나로 합쳐 구성

참조
### [nestjs/mappled-types](https://github.com/nestjs/mapped-types)