# `level 2` 소수 찾기

## 문제 설명
한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

## 제한사항
- numbers는 길이 1 이상 7 이하인 문자열입니다.
- numbers는 0~9까지 숫자만으로 이루어져 있습니다.
- "013"은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.

## 입출력 예
![image](https://user-images.githubusercontent.com/122213470/230832867-a65774aa-8883-4fe8-b7dd-3cdb43d6c726.png)

## Other's Solution

Point:
- `range()` 안에는 정수만!
- `extend`
  + `from itertools import permutations`
  + `result.extend(list(permutations(a, i)))`
  + `result += permutations(a, i)` 과 같은 결과
  + `result.append(list(permutations(a, i)))` 는 이중 리스트가 됨
- `.append`는 원소 하나만 추가, `.extend`와 `+=`는 그냥 조인해줌
- `int`를 해줘야 011 과 11 을 같은 값으로 인식
- `set`은 인덱싱이 불가

```python

```

## 주영's Solution

```python
def solution(numbers):
    comb = []
    for i in range(1, len(numbers)+1):
        comb += permutations(numbers, i)   # extend와 같음
        
    result = list(set([int(''.join(i))for i in comb]))
    
    is_prime = [1] * len(result)
    
    for i in range(len(result)):
        if result[i] <= 1:
            is_prime[i] = 0
        for j in range(2, int(np.sqrt(result[i]))+1):   # int() 있어야 함
            if result[i] % j == 0:
                is_prime[i] = 0
    
    return sum(is_prime)
```

## 서연's Solution

- 서연's temp == 주영's is_prime
- 굳이 `num = [x for x in numbers]` 이렇게 할 필요가 없었음..! 문자열도 iterative 하기 때문

```python
from itertools import permutations
def solution(numbers):
    answer = 0
    # 문자열을 분리해서 리스트로 저장
    num = [x for x in numbers]   
    # 순열로 모든 조합 생성
    L = [] # 모든 조합 담을 리스트
    for i in range(len(numbers)): # 1개부터 numbers 자릿수까지의 수를 생성 
        p = permutations(num, i+1)
        L += [int(''.join(x)) for x in p] # 하나의 문자열로 합치고 정수로 변환
    # L 에는 0,1,1,1,1,... , 110 이 담겨있음 -> 중복제거
    for n in set(L):
        # 0과 1은 소수가 아님
        temp = 1
        if n <=1:
            temp = 0
        for k in range(2,int(n**0.5)+1): # 제곱근 범위까지 탐색
            if n%k==0: #나눠지면 소수가 아님
                temp=0
                break
        if temp == 1:
            answer += 1                
    return answer
```
