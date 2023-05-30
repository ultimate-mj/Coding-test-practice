# `level 2` 튜플

## 문제 설명
셀수있는 수량의 순서있는 열거 또는 어떤 순서를 따르는 요소들의 모음을 튜플(tuple)이라고 합니다. n개의 요소를 가진 튜플을 n-튜플(n-tuple)이라고 하며, 다음과 같이 표현할 수 있습니다.

- (a1, a2, a3, ..., an)

튜플은 다음과 같은 성질을 가지고 있습니다.

1. 중복된 원소가 있을 수 있습니다. ex : (2, 3, 1, 2)
2. 원소에 정해진 순서가 있으며, 원소의 순서가 다르면 서로 다른 튜플입니다. ex : (1, 2, 3) ≠ (1, 3, 2)
3. 튜플의 원소 개수는 유한합니다.

원소의 개수가 n개이고, 중복되는 원소가 없는 튜플 `(a1, a2, a3, ..., an)`이 주어질 때(단, a1, a2, ..., an은 자연수), 이는 다음과 같이 집합 기호 '{', '}'를 이용해 표현할 수 있습니다.

- {{a1}, {a1, a2}, {a1, a2, a3}, {a1, a2, a3, a4}, ... {a1, a2, a3, a4, ..., an}}

예를 들어 튜플이 (2, 1, 3, 4)인 경우 이는

- {{2}, {2, 1}, {2, 1, 3}, {2, 1, 3, 4}}

와 같이 표현할 수 있습니다. 이때, 집합은 원소의 순서가 바뀌어도 상관없으므로

- {{2}, {2, 1}, {2, 1, 3}, {2, 1, 3, 4}}
- {{2, 1, 3, 4}, {2}, {2, 1, 3}, {2, 1}}
- {{1, 2, 3}, {2, 1}, {1, 2, 4, 3}, {2}}

는 모두 같은 튜플 (2, 1, 3, 4)를 나타냅니다.

특정 튜플을 표현하는 집합이 담긴 문자열 s가 매개변수로 주어질 때, s가 표현하는 튜플을 배열에 담아 return 하도록 solution 함수를 완성해주세요.

## [제한사항]
- s의 길이는 5 이상 1,000,000 이하입니다.
- s는 숫자와 '{', '}', ',' 로만 이루어져 있습니다.
- 숫자가 0으로 시작하는 경우는 없습니다.
- s는 항상 중복되는 원소가 없는 튜플을 올바르게 표현하고 있습니다.
- s가 표현하는 튜플의 원소는 1 이상 100,000 이하인 자연수입니다.
- return 하는 배열의 길이가 1 이상 500 이하인 경우만 입력으로 주어집니다.

## 입출력 예
![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/5ec26bca-8839-453b-94a6-31a1334f67ea)

## My Solution. 틀림

Idea:
- 각 string에서 ','를 빼고 list로 만들자
  - 문제!! {20, 111} 인 경우 ['2', '0', '1', '1', '1'] 로 됨..!
- use `sort(lambda: )`

알고리즘:
1. 길이가 짧은 집합 순서대로 나열하고
2. 다음 집합에서 겹치지 않는 원소를 찾아 튜플에 넣기

```python
def solution(s):
    answer = []
    s = s.strip('{}').split('},{')  #리스트 안에 string 형태로 각 집합이 있음
    for i in range(len(s)):
        s[i] = s[i].replace(',', '') #각 string에서 ',' 를 빼주기
    s = list(map(list, s)) #각 string을 list로 바꾸기 [['2'], ['2', '1']] 이런 식으로 있음
    
    s.sort(key = lambda x: len(x)) #원소 순서대로 sort
    answer.append(int(s[0][0]))
    for i in range(1, len(s)):
        for j in range(len(s[i])):  
            if s[i][j] not in s[i-1]: #이전 원소에 없으면 답에 넣기
                answer.append(int(s[i][j]))

    return answer
```

## Other's Solution. 

Idea:
- ',' 기준으로 split 하는 것을 첫 번째 루프 돌 때 하기!

```python
def solution(s):
    answer = []
    s = s[2:-2]
    s = s.split("},{")
    s.sort(key = len)
    for i in s:
        ii = i.split(',')
        for j in ii:
            if int(j) not in answer:
                answer.append(int(j))
    return answer
```
