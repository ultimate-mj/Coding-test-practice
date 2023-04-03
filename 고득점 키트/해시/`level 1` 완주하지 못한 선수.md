# `level 1` 완주하지 못한 선수 
https://school.programmers.co.kr/learn/courses/30/lessons/42576

## 문제 설명

수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

## 제한사항
- 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
- completion의 길이는 participant의 길이보다 1 작습니다.
- 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
- 참가자 중에는 동명이인이 있을 수 있습니다.

![image](https://user-images.githubusercontent.com/122213470/229139309-17d4195b-364b-4bf9-bdf3-bd7929e05e17.png)

## My Solution 1. (실페)

알고리즘
- participant 에서 completion의 원소를 하나씩 pop 하기 (중복되는 것이 있으므로 pop 하는 것을 생각)

Point:
- Use `enumerate`
- Use `pop`
- Use `.index` - **이거 검색해봄**
- 동명이인이 있을 수 있음에 유의
- 출력은 리스트가 아니라 string의 형태로 해야 함

결과:
- 정확성 테스트에서는 모두 통과되지만 효율성 테스트를 하나도 통과하지 못했다.

```python
def solution(participant, completion):
    for i, x in enumerate(completion):
        participant.pop(participant.index(x))
    answer = participant[0]
    return answer
```

## My Solution 2. (실패)

Point:
- Use `del` instead of `pop`

결과:
- 마찬가지로 시간 초과

```python
def solution(participant, completion):
    for i, x in enumerate(completion):
        del participant[participant.index(x)]
    answer = participant[0]
    return answer
```

## My Solution 3. (더 실패)

알고리즘:
- 각 리스트를 정렬해서 순서대로 탐색했을 때 다른 값이 나온다면 participant의 해당 값을 return
- 단, participant의 마지막에 answer이 있는 경우를 따로 처리해야 함

결과:
- 시간 초과 & 정확성 테스트 7개 중 5개 실패

```python
def solution(participant, completion):
    participant.sort()
    completion.sort()
    answer = []
    for i, x in enumerate(completion):
        if x != participant[i]:
            answer = participant[i]
    if answer == []:
        answer = participant[-1]
    return answer
```

------

## Other's solution 1. Use loop
https://coding-grandpa.tistory.com/85

```python
def solution(participant, completion):
    answer = ''

    # 1. 두 list를 sorting한다
    participant.sort()
    completion.sort()

    # 2. completeion list의 len만큼 participant를 찾아서 없는 사람을 찾는다
    for i in range(len(completion)):
        if(participant[i] != completion[i]):
            return participant[i]

    # 3. 전부 다 돌아도 없을 경우에는 마지막 주자가 완주하지 못한 선수이다.
    return participant[len(participant)-1]
```

## Other's solution 2. Use hash

```python
def solution(participant, completion):
    hashDict = {}
    sumHash = 0
    
    # 1. Hash : Participant의 dictionary 만들기
    # 2. Participant의 sum(hash) 구하기
    for part in participant:
        hashDict[hash(part)] = part
        sumHash += hash(part)
    
    # 3. completion의 sum(hash) 빼기
    for comp in completion:
        sumHash -= hash(comp)
    
    # 4. 남은 값이 완주하지 못한 선수의 hash 값이 된다

    return hashDict[sumHash]
```

## Other's solution 3. Use Counter

```python
import collections
def solution(participant, completion):
    # 1. participant의 Counter를 구한다
    # 2. completion의 Counter를 구한다
    # 3. 둘의 차를 구하면 정답만 남아있는 counter를 반환한다
    answer = collections.Counter(participant) - collections.Counter(completion)
    
    # 4. counter의 key값을 반환한다
    return list(answer.keys())[0]
```

![image](https://user-images.githubusercontent.com/122213470/229399874-5965cbb6-81d9-4c68-86f7-3f615389b3d1.png)

자료 출처: https://coding-grandpa.tistory.com/85
