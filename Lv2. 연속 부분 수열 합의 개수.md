# `level 2` 연속 부분 수열 합의 개수

## 문제 설명
철호는 수열을 가지고 놀기 좋아합니다. 어느 날 철호는 어떤 자연수로 이루어진 원형 수열의 연속하는 부분 수열의 합으로 만들 수 있는 수가 모두 몇 가지인지 알아보고 싶어졌습니다. 원형 수열이란 일반적인 수열에서 처음과 끝이 연결된 형태의 수열을 말합니다. 예를 들어 수열 [7, 9, 1, 1, 4] 로 원형 수열을 만들면 다음과 같습니다.

![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/2a0ec73d-a016-4e8f-b986-b2c5ca37c58d)

원형 수열은 처음과 끝이 연결되어 끊기는 부분이 없기 때문에 연속하는 부분 수열도 일반적인 수열보다 많아집니다.
원형 수열의 모든 원소 `elements`가 순서대로 주어질 때, 원형 수열의 연속 부분 수열 합으로 만들 수 있는 수의 개수를 return 하도록 solution 함수를 완성해주세요.

## 제한사항
- 3 ≤ elements의 길이 ≤ 1,000
- 1 ≤ elements의 원소 ≤ 1,000

## 입출력 예
![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/f2369bfd-8e90-4632-89fb-b4fa30bdcf2a)

## My Solution.

Idea:
- list의 앞부분을 떼어서 뒤에 붙이고 sum을 하자

주의:
- 리스트에 정수값을 넣을 때에는 `.append`
- 리스트와 리스트를 합칠 때에는 `+`

```python
def solution(elements):
    sums = []
    sums.append(sum(elements))
    for i in range(1, len(elements)):
        new_list = elements + elements[0:i+1]
        for j in range(0, len(elements)):
            sums.append(sum(new_list[j:j+i]))
    return(len(set(sums)))
```
