# 에라토스네테스의 체
- 소수를 판별하는 가장 빠른 알고리즘
- 대량의 소수를 한꺼번에 판별할 때 적합

## 방법
1. 배열을 생성하여 초기화
2. 소수의 배수에 해당하는 수를 모두 지움(자기 자신은 지우지 않고 이미 지워진 수는 건너뜀)
3. 남아있는 수를 모두 출력

### 코드
```java
int num = 10;
boolean[] arr = new boolean[num + 1];

for(int i=2; i*i<=num; i++){
    if(!arr[i]) {
    	for(int j=i*i; j<=num; j+=i) {
    		arr[j] = true;
    	}
    }
}
				
for(int i=2; i<=num; i++) {
	if(!arr[i]) {
		System.out.println(i);
	}
}
```