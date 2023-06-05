# `level 3` 이중우선순위큐

## 문제 설명
이중 우선순위 큐는 다음 연산을 할 수 있는 자료구조를 말합니다.

![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/3f9673d4-2e91-476a-b6ab-93a464e6e96e)

이중 우선순위 큐가 할 연산 operations가 매개변수로 주어질 때, 모든 연산을 처리한 후 큐가 비어있으면 [0,0] 비어있지 않으면 [최댓값, 최솟값]을 return 하도록 solution 함수를 구현해주세요.

## 제한사항
- operations는 길이가 1 이상 1,000,000 이하인 문자열 배열입니다.
- operations의 원소는 큐가 수행할 연산을 나타냅니다.
  + 원소는 “명령어 데이터” 형식으로 주어집니다.- 최댓값/최솟값을 삭제하는 연산에서 최댓값/최솟값이 둘 이상인 경우, 하나만 삭제합니다.
- 빈 큐에 데이터를 삭제하라는 연산이 주어질 경우, 해당 연산은 무시합니다.

## 입출력 예
![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/070aec70-8e59-4248-b1d2-b6b783e82aca)

### 입출력 예 설명 1.
- 16과 -5643을 삽입합니다.
- 최솟값을 삭제합니다. -5643이 삭제되고 16이 남아있습니다.
- 최댓값을 삭제합니다. 16이 삭제되고 이중 우선순위 큐는 비어있습니다.
- 우선순위 큐가 비어있으므로 최댓값 삭제 연산이 무시됩니다.
- 123을 삽입합니다.
- 최솟값을 삭제합니다. 123이 삭제되고 이중 우선순위 큐는 비어있습니다.

따라서 [0, 0]을 반환합니다.

### 입출력 예 설명 2.
- -45와 653을 삽입후 최댓값(653)을 삭제합니다. -45가 남아있습니다.
- -642, 45, 97을 삽입 후 최댓값(97), 최솟값(-642)을 삭제합니다. -45와 45가 남아있습니다.
- 333을 삽입합니다.

이중 우선순위 큐에 -45, 45, 333이 남아있으므로, [333, -45]를 반환합니다.

## My Solution

알고리즘:
1. 명령어가 `I`, `D`, `D -` 중 무엇인지 파악한다.
2. 명령어 뒤에 나오는 숫자를 integer 형태로 바꾸어 삽입/삭제한다.
  2.1. 빈 큐에서 데이터를 삭제하는 경우를 따로 처리한다.

Idea:
- 리스트에서 최솟값을 삭제하기:
 ```
 list = [2, 5, 1, 4]
 list.pop(list.index(min(list)))
 ```
`list.pop(index)` 보다는 `que.remove(item)` 을 쓰자!
```
from collections import deque
que = deque([2, 5, 1, 4])
que.remove(min(que))
```

```python
for i in operations:
        if i[0] == 'I':
            que.append(int(i[2:]))
        else:
          if que:
            if i[2] == '-':
              que.remove(min(que))
            else:
              que.remove(max(que))

if que:
  print([max(que), min(que)])
else:
  print([0,0])
```
