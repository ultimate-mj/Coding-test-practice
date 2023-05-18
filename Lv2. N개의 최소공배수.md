# `level 2` N개의 최소공배수

## 문제 설명
두 수의 최소공배수(Least Common Multiple)란 입력된 두 수의 배수 중 공통이 되는 가장 작은 숫자를 의미합니다. 예를 들어 2와 7의 최소공배수는 14가 됩니다. 정의를 확장해서, n개의 수의 최소공배수는 n 개의 수들의 배수 중 공통이 되는 가장 작은 숫자가 됩니다. n개의 숫자를 담은 배열 arr이 입력되었을 때 이 수들의 최소공배수를 반환하는 함수, solution을 완성해 주세요.

## 제한 사항
- arr은 길이 1이상, 15이하인 배열입니다.
- arr의 원소는 100 이하인 자연수입니다.

## 입출력 예
![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/02c9bd5b-356f-43d6-92c0-b26089f634c9)

## Solution 1.

Idea:
- 최대공약수를 구하는 함수: `gcd`
  + `from math import gcd` 해줘야 함!!
- A, B의 최소공배수 = A, B의 곱 / 최대공약수
  + 이거를 모든 수에 대해 돌아가면서

!주의: 
- `/` 를 하면 `float` 형태로 나와서 `//` 사용해야 함

```python
def solution(arr):
    from math import gcd
    answer = arr[0]
    
    for i in arr:
        answer = answer * i // gcd(answer, i)
    return answer
```


## Solution 2.
https://velog.io/@insutance/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4Python-N%EA%B0%9C%EC%9D%98-%EC%B5%9C%EC%86%8C%EA%B3%B5%EB%B0%B0%EC%88%98

Idea:
- 가장 큰 수에 1부터 곱하면서 모든 수에 대해 나머지가 0일 때까지 n을 증가시킴

```python
def solution(arr):
    answer = 0
    n = 1                           
    
    while True:
        answer = max(arr) * n       # 가장 큰 수의 배수 기준으로 최소공배수를 구함.
        result = True               # if result=True: 최소공배수    else: 최소공배수가 아님
        for num in arr:
            if answer % num != 0:   
                result = False      # answer가 나누어 떨어지지 않으면 result=False로 변경 후 break
                break
        if result:                  # result 판별 True이면 while True문을 빠져나옴
            break                   
        n += 1
        
    return answer
```
