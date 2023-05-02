# `level 2` JadenCase 문자열 만들기

## 문제 설명

JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 단, 첫 문자가 알파벳이 아닐 때에는 이어지는 알파벳은 소문자로 쓰면 됩니다. (첫 번째 입출력 예 참고)
문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

## 제한 조건
- s는 길이 1 이상 200 이하인 문자열입니다.
- s는 알파벳과 숫자, 공백문자(" ")로 이루어져 있습니다.
  + 숫자는 단어의 첫 문자로만 나옵니다.
  + 숫자로만 이루어진 단어는 없습니다.
  + 공백문자가 연속해서 나올 수 있습니다.

## 입출력 예
![image](https://user-images.githubusercontent.com/122213470/235564059-b137a849-843d-444b-99c2-c45b19d53e71.png)

## My Solution 1. `runtime error`

- Defined a function to use `map`

```python
def solution(s):
    temp = s.split(' ')
    def Jaden(a):
        a = a[0].upper() + a.lower()[1:]
        return a
    answer = ' '.join(list(map(Jaden, temp)))
    return answer
```

## My Solution 2. `runtime error`

- use `for` loop instead

```python
def solution(s):
    temp = s.split(' ')
    lists =[]
    for i in range(len(temp)):
        lists.append(temp[i][0].upper() + temp[i].lower()[1:])
    answer = ' '.join(lists)
    return answer
```

## My Solution 3.

- use `.capitalize()` !!

```python
def solution(s):
    temp = s.split(' ')
    lists =[]
    for i in range(len(temp)):
        lists.append(temp[i].capitalize())
    answer = ' '.join(lists)
    return answer
```

## Useful concept

1. `.upper()` : 모든 알파벳을 대문자로
2. `.capitalize()` : 맨 첫 글자만 대문자로
3. `.title()` : 알파벳 외의 문자로 나누어져 있는 영단어들의 첫 글자를 모두 대문자로








