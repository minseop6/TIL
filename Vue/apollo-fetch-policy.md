# Fetch Policy
- Data를 가져오는 주체와 cache에 저장 여부를 설정하는 옵션

- ## chche-first
    - `fetch-policy` 옵션의 default
    - 기본적으로 cache data를 가져옴
    - cache data가 없을 경우에 network에서 데이터를 받아오고 cache에 저장
- ## cache-and-network
    - 기본적으로 cache data 가 있을경우 가져옴
    - 그 후에 network로 부터 data를 받아오고 cache에 저장
- ## cache-only
    - cache data를 가져옴
    - cache data가 없을 경우에는 fail
- ## network-only
    - nework에서 data를 가져옴
    - 그후에 cache에 저장
- ## no-cache
    - nework에서 data를 가져옴
    - network 호출에 실패해도 cache에 저장하지 않음
