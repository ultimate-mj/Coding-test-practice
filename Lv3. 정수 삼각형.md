# `level 3` 정수 삼각형

## 문제 설명

![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/6106b784-a4e9-47e4-b6ba-d5bf2fc96b65)

위와 같은 삼각형의 꼭대기에서 바닥까지 이어지는 경로 중, 거쳐간 숫자의 합이 가장 큰 경우를 찾아보려고 합니다. 아래 칸으로 이동할 때는 대각선 방향으로 한 칸 오른쪽 또는 왼쪽으로만 이동 가능합니다. 예를 들어 3에서는 그 아래칸의 8 또는 1로만 이동이 가능합니다.

삼각형의 정보가 담긴 배열 triangle이 매개변수로 주어질 때, 거쳐간 숫자의 최댓값을 return 하도록 solution 함수를 완성하세요.

## 제한사항
- 삼각형의 높이는 1 이상 500 이하입니다.
- 삼각형을 이루고 있는 숫자는 0 이상 9,999 이하의 정수입니다.

## 입출력 예
![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/4770cdc7-facf-4f44-b3b3-e918e03c9f01)

## Solution.
https://soohyun6879.tistory.com/157

- use `dynamic programming`

```python
def solution(triangle):

    for i in range(1, len(triangle)): # i = 몇번째 줄인지
        for j in range(i+1): # j = 줄 안에서 인덱스
            if j == 0: # 가장 왼쪽인 경우
                triangle[i][j] += triangle[i-1][j]
            elif j == i: # 가장 오른쪽인 경우
                triangle[i][j] += triangle[i-1][-1]
            else: # 가운데인 경우
                triangle[i][j] += max(triangle[i-1][j-1], triangle[i-1][j])
                
    return max(triangle[-1])
```

```python
def solution(triangle):
    triangle = [[0] + line + [0] for line in triangle]
    
    for i in range(1, len(triangle)):
        for j in range(1, i+2):
            triangle[i][j] += max(triangle[i-1][j-1], triangle[i-1][j])
            
    return max(triangle[-1])
```
