# `level 2` 카펫

## 문제 설명
Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 노란색으로 칠해져 있고 테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.
![image](https://user-images.githubusercontent.com/122213470/230834834-38e5d698-da50-49b8-ae7a-34f740998e77.png)

Leo는 집으로 돌아와서 아까 본 카펫의 노란색과 갈색으로 색칠된 격자의 개수는 기억했지만, 전체 카펫의 크기는 기억하지 못했습니다.

Leo가 본 카펫에서 갈색 격자의 수 brown, 노란색 격자의 수 yellow가 매개변수로 주어질 때 카펫의 가로, 세로 크기를 순서대로 배열에 담아 return 하도록 solution 함수를 작성해주세요.

## 제한사항
- 갈색 격자의 수 brown은 8 이상 5,000 이하인 자연수입니다.
- 노란색 격자의 수 yellow는 1 이상 2,000,000 이하인 자연수입니다.
- 카펫의 가로 길이는 세로 길이와 같거나, 세로 길이보다 깁니다.

## 입출력 예
![image](https://user-images.githubusercontent.com/122213470/230835040-16982f61-627d-404b-b057-5888ca438bf7.png)

## 유경's Solution
- 제일 빠름!!
- `for`문 안에 `if`문 있으면 `break` 쓰는게 훨씬 빠름!!

```python
def solution(brown, yellow):
    answer = [3,3]  #yellow=1 이면 [3,3]만 돼서
    for i in range(1, yellow//2+1):
        if yellow % i == 0:
            b_width = max(yellow//i, i) + 2
            b_height = min(yellow//i, i) + 2
            if b_width*b_height == (brown+yellow):
                answer = [b_width, b_height]
                break

    return answer
```

## 주영's Solution

```python
def solution(brown, yellow):
    yellows = [x for x in range(1, yellow+1) if yellow % x == 0]
    new = [x+2 for x in yellows] 
    
    for i in new:
        for j in new:
            if i * j == brown + yellow:
                return [j, i]
```

## 서연's Solution

```python
def solution(brown, yellow):
    # yellow의 개수 24 : 1*24, 2*12,.... 가능 -> 모든 약수 조합 구하기
    # 가로 세로는 yellow가로+2, yellow세로+2
    # brown+ yellow는 yellow가로+2, yellow세로+2와 같음
    num1 = [x for x in range(1,yellow+1) if yellow%x==0] # 1,2,3
    num2 = [yellow/x for x in num1] # 24, 12, 8
    for i in range(len(num1)):
        a = num1[i]+2
        b = num2[i]+2
        if brown + yellow == a*b:
            return [b, a]
```


## Useful Concepts

- `continue`: 다음 순번으로 넘어가라
- `pass`: 뒤의 것도 수행함, 에러가 나오더라도 그냥 넘겨버림
