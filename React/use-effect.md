# useEffect
- 컴포넌트가 렌더링 될 때마다 사이드 이펙트를 실행시킬 수 있도록 해줌

```js
const Counter =  () => {
    const [count, setCount] = useState(0);

    useEffect(() => {
        console.log('Rendering');
        console.log(`count: ${count}`)
    })

    return (
    <div className="Counter">
      <button type="button" onClick={setCount(count + 1)}>
        +
      </button>
      <span>&nbsp;{count}&nbsp;</span>
      <button type="button" onClick={setCount(count - 1)}>
        -
      </button>
    </div>
  );
}
```

- 마운트될 때만 실행하려면 2번째 파라미터에 빈배열을 넣어주면됨

```js
useEffect(() => {
    console.log('Rendering');
    console.log(`count: ${count}`)
}, [])
```

- 업데이트 될 때만 실행하려면 2번째 파라미터에 체크할 변수를 넣어주면됨

```js
useEffect(() => {
    console.log('Rerendering');
    console.log(`count: ${count}`)
}, [count])
```

- rerending되기전에 특정 사이드 이펙트를 실행하려면 cleanup 함수를 반환

```js
useEffect(() => {
    console.log('Render');
    console.log(`count: ${count}`)

    return () => {
        console.log('cleanup');
    }
})
```