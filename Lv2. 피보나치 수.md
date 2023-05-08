# `level 2` 피보나치 수

## 문제 설명
피보나치 수는 F(0) = 0, F(1) = 1일 때, 1 이상의 n에 대하여 F(n) = F(n-1) + F(n-2) 가 적용되는 수 입니다.

예를들어

- F(2) = F(0) + F(1) = 0 + 1 = 1
- F(3) = F(1) + F(2) = 1 + 1 = 2
- F(4) = F(2) + F(3) = 1 + 2 = 3
- F(5) = F(3) + F(4) = 2 + 3 = 5

와 같이 이어집니다.

2 이상의 n이 입력되었을 때, n번째 피보나치 수를 1234567으로 나눈 나머지를 리턴하는 함수, solution을 완성해 주세요.

## 제한 사항
n은 2 이상 100,000 이하인 자연수입니다.

## 입출력 예
![image](https://user-images.githubusercontent.com/122213470/236729598-f9d733f6-86f3-432e-a1af-0129622b52a4.png)

## My Solution 1. Runtime error

Idea:
- Use Recursion 재귀함수 사용!

```python
def solution(n):
    if n < 2:
        return n
    else:
        return solution(n-1) + solution(n-2)
```

피보나치 수 연습 힌트 모음: (비슷한 에러가 뜨는 실수를 많이들 하는 듯하다)
https://school.programmers.co.kr/learn/courses/14743/14743-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%97%B0%EC%8A%B5-%ED%9E%8C%ED%8A%B8-%EB%AA%A8%EC%9D%8C%EC%A7%91?itm_content=lesson12945
