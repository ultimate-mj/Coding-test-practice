# `level 3` 최고의 집합

## 문제 설명
자연수 n 개로 이루어진 중복 집합(multi set, 편의상 이후에는 "집합"으로 통칭) 중에 다음 두 조건을 만족하는 집합을 최고의 집합이라고 합니다.

1. 각 원소의 합이 S가 되는 수의 집합
2. 위 조건을 만족하면서 각 원소의 곱 이 최대가 되는 집합

예를 들어서 자연수 2개로 이루어진 집합 중 합이 9가 되는 집합은 다음과 같이 4개가 있습니다.
{ 1, 8 }, { 2, 7 }, { 3, 6 }, { 4, 5 }
그중 각 원소의 곱이 최대인 { 4, 5 }가 최고의 집합입니다.

집합의 원소의 개수 n과 모든 원소들의 합 s가 매개변수로 주어질 때, 최고의 집합을 return 하는 solution 함수를 완성해주세요.

## 제한사항
- 최고의 집합은 오름차순으로 정렬된 1차원 배열(list, vector) 로 return 해주세요.
- 만약 최고의 집합이 존재하지 않는 경우에 크기가 1인 1차원 배열(list, vector) 에 -1 을 채워서 return 해주세요.
- 자연수의 개수 n은 1 이상 10,000 이하의 자연수입니다.
- 모든 원소들의 합 s는 1 이상, 100,000,000 이하의 자연수입니다.

## 입출력 예
![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/62f5dc12-164e-4fee-9fcc-0cdb562e9498)

## My Solution 1. 시간 초과 (정확성 70점, 효율성 0점)

알고리즘:
 - n=5, s=23인 경우를 생각해보면 [5, 5, 5, 4, 4] 의 곱이 최대임
 - n=5, s=22인 경우에는 [5, 5, 4, 4, 4] 의 곱이 최대임
 
 $\rightarrow$ a = s를 n으로 나눈 것의 몫, b = s를 n으로 나눈 것의 나머지라 할 때, answer = [rep(a, n-b개), rep(a+1, b개)]
    
주의:
- `np.array()` 의 각 원소 타입은 `numpy.int64`이다
  + `list(np.array())`로 해도 원소는 여전히 `numpy.int64`로 존재하기 때문에 내부 원소까지 모두 `int`형으로 변환해야 한다!!

Idea:
- Use `np.repeat`

```python
def solution(n, s):
    import numpy as np
    a = int(s//n)
    b = int(s%n)
    if a == 0:
        answer = [-1]
        return answer
    answer = list(int(x) for x in np.repeat([a], n-b))
    answer += list(int(x) for x in np.repeat([a+1], b))
    return answer
```

## My Solution 2.

Idea:
- Use `repeat`
  + `from itertools import repeat`

```python
def solution(n, s):
    from itertools import repeat
    a = int(s//n)
    b = int(s%n)
    if a == 0:
        answer = [-1]
        return answer
    answer = list(repeat(a, n-b))
    answer += list(repeat(a+1, b))
    return answer

```


