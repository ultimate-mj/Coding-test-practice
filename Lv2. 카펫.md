# `level 2` 카펫

## 문제 설명
Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 노란색으로 칠해져 있고 테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.
![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/4889a9fa-04fd-41f6-ba1a-1ebc9d85924a)

Leo는 집으로 돌아와서 아까 본 카펫의 노란색과 갈색으로 색칠된 격자의 개수는 기억했지만, 전체 카펫의 크기는 기억하지 못했습니다.

Leo가 본 카펫에서 갈색 격자의 수 brown, 노란색 격자의 수 yellow가 매개변수로 주어질 때 카펫의 가로, 세로 크기를 순서대로 배열에 담아 return 하도록 solution 함수를 작성해주세요.

## 제한사항
- 갈색 격자의 수 brown은 8 이상 5,000 이하인 자연수입니다.
- 노란색 격자의 수 yellow는 1 이상 2,000,000 이하인 자연수입니다.
- 카펫의 가로 길이는 세로 길이와 같거나, 세로 길이보다 깁니다.

## 입출력 예
![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/53cd582f-afae-41c3-9920-8f365139db4a)

## My Solution

Idea:
1. 카펫의 크기가 [가로, 세로] = [a, b] 이라면
  + brown = 2(a+b-2)
  + yellow = (a-2) $\times$ (b-2) 개 있다.
2. 주어진 정보가 brown, yellow 이므로
  + a+b = brown / 2 + 2 로 구하고
  + a, b 의 모든 짝 중 (a-2) $\times$ (b-2) = yellow 를 만족하는 쌍을 구한다.

주의: 
- a $\ge$ b
- `range` 안에는 `int` 만 들어갈 수 있음
- `range(a, b)` 는 `a`부터 `b-1`까지라서 마지막에 `+1` 필요

```python
def solution(brown, yellow):
    sums = brown / 2 + 2
    for i in range(1, int(sums//2)+1):
        b = i
        a = sums - i
        if (a-2)*(b-2) == yellow:
            return [a, b]
```
