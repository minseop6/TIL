# Circular Dependency
## 원인
- NestJS Module이 서로 import 하면 순환 의존성 문제 발생

```js
@Module({
  imports: [PostModule)],
  providers: [
    CommentResolver,
    CommentSubResolver,
    CommentService,
    CommonCommentService,
  ],
  exports: [CommentService],
})
export class CommentModule {}

```

```js
@Module({
  imports: [CommentModule)],
  providers: [
    PostResolver,
    PostSubResolver,
    PostService,
    CommonPostService,
  ],
  exports: [PostService],
})
export class PostModule {}

```

## 해결 방법
- `forwardRef` 메소드를 사용해서 해결

```js
@Module({
  imports: [forwardRef(() => PostModule)],
  providers: [
    CommentResolver,
    CommentSubResolver,
    CommentService,
    CommonCommentService,
  ],
  exports: [CommentService],
})
export class CommentModule {}

```

```js
@Module({
  imports: [forwardRef(() => CommentModule)],
  providers: [
    PostResolver,
    PostSubResolver,
    PostService,
    CommonPostService,
  ],
  exports: [PostService],
})
export class PostModule {}

```