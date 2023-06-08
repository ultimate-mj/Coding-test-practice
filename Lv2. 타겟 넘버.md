# `level 2` 타겟 넘버
https://school.programmers.co.kr/learn/courses/30/lessons/43165

## 문제 설명
n개의 음이 아닌 정수들이 있습니다. 이 정수들을 순서를 바꾸지 않고 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.
```
-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3
```
사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

## 제한사항
- 주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
- 각 숫자는 1 이상 50 이하인 자연수입니다.
- 타겟 넘버는 1 이상 1000 이하인 자연수입니다.

## 입출력 예
![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/49974a76-05d0-4665-a7d1-4c15f1400316)

### 입출력 예 설명2
```
+4+1-2+1 = 4
+4-1+2-1 = 4
```
- 총 2가지 방법이 있으므로, 2를 return 합니다.

## Solution.
https://daeun-computer-uneasy.tistory.com/69?category=1053494 참고

Idea:
- use `BFS`
  + 이진 트리 형식으로 뻗어나갈 수 있는 문제는 `DFS/BFS`로 접근할 수 있음을 염두에 두자!!

```python
def solution(numbers, target):
    answer = 0
    sums = [0]
    for i in numbers:
        temp = []
        for j in sums:
            temp.append(j + i)  # 더하는 경우
            temp.append(j - i)  # 빼는 경우
            sums = temp
    for k in sums:
        if k == target:
            answer += 1
    return answer
```

