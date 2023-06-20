# `level 2` [3차] n진수 게임

## 문제 설명

튜브가 활동하는 코딩 동아리에서는 전통적으로 해오는 게임이 있다. 이 게임은 여러 사람이 둥글게 앉아서 숫자를 하나씩 차례대로 말하는 게임인데, 규칙은 다음과 같다.

1. 숫자를 0부터 시작해서 차례대로 말한다. 첫 번째 사람은 0, 두 번째 사람은 1, … 열 번째 사람은 9를 말한다.
2. 10 이상의 숫자부터는 한 자리씩 끊어서 말한다. 즉 열한 번째 사람은 10의 첫 자리인 1, 열두 번째 사람은 둘째 자리인 0을 말한다.

이렇게 게임을 진행할 경우,

`0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 1, 0, 1, 1, 1, 2, 1, 3, 1, 4, …`

순으로 숫자를 말하면 된다.

한편 코딩 동아리 일원들은 컴퓨터를 다루는 사람답게 이진수로 이 게임을 진행하기도 하는데, 이 경우에는

`0, 1, 1, 0, 1, 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 1, …`

순으로 숫자를 말하면 된다.

이진수로 진행하는 게임에 익숙해져 질려가던 사람들은 좀 더 난이도를 높이기 위해 이진법에서 십육진법까지 모든 진법으로 게임을 진행해보기로 했다. 
숫자 게임이 익숙하지 않은 튜브는 게임에 져서 벌칙을 받는 굴욕을 피하기 위해, 자신이 말해야 하는 숫자를 스마트폰에 미리 출력해주는 프로그램을 만들려고 한다. 튜브의 프로그램을 구현하라.

## 입력 형식
진법 n, 미리 구할 숫자의 갯수 t, 게임에 참가하는 인원 m, 튜브의 순서 p 가 주어진다.

- 2 ≦ n ≦ 16
- 0 ＜ t ≦ 1000
- 2 ≦ m ≦ 100
- 1 ≦ p ≦ m

## 출력 형식
튜브가 말해야 하는 숫자 `t`개를 공백 없이 차례대로 나타낸 문자열. 단, `10`~`15`는 각각 대문자 `A`~`F`로 출력한다.

## 입출력 예시
![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/fca8efb5-2435-4ce6-a40a-579e1e18fd93)

## Other's Solution 1.
https://velog.io/@sem/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-LEVEL2-n%EC%A7%84%EC%88%98-%EA%B2%8C%EC%9E%84-Python

```python
#n진수로 바꾸는 함수 만들기
def convert(num, base):
    temp = "0123456789ABCDEF"
    q, r = divmod(num, base)

    if q == 0:
        return temp[r]
    else:
        # q를 base로 변환
        # 즉, n진수의 다음 자리를 구함
        return convert(q, base) + temp[r]
    
def solution(n, t, m, p):
    answer = ''
    test = ''

    # n진수로 바꾼 숫자를 문자열로 나열
    for i in range(m*t):
        test += str(convert(i, n))

    # 튜브가 말해야 하는 숫가 t개를 answer에 넣고 사람 수인 m개씩 건너뛰기
    while len(answer) < t:
        answer += test[p-1]
        p += m
        
    return answer
```

## Other's Solution 2.

https://velog.io/@djagmlrhks3/Algorithm-Programmers-3%EC%B0%A8-n%EC%A7%84%EC%88%98-%EA%B2%8C%EC%9E%84-by-Python

```python
def solution(n, t, m, p):
    answer = ''
    length = m * t
    candidate = '0'
    num = 0
    alpha = 'ABCDEF'
    
    while len(candidate) < length: #length 길이보다 작을 때 까지 n진법으로 변환!
        res = ''
        number = num
        while True: # 자연수 number를 n진법으로 변환하는 반복문 
            if number == 0: # 더 이상 나누지 못하면 break
                break
            if number % n:
                if number % n >= 10: # 10~15값이면 alpha와 매핑
                    res += alpha[(number%n) % 10]
                else: # 나머지 값을 res에 담는다.
                    res += str(number % n)
            else:
                res += '0'
            number //= n
        num += 1
        candidate += res[::-1] # 역순으로 담았기 때문에 슬라이싱([::-1])을 이용하여 candidate에 담는다.
    for i in range(p-1, length, m): answer += candidate[i] # 튜브의 순서에 해당하는 숫자를 answer에 담는다!
    return answer
```


## Useful Concept

1. n진수 -> 10진수 : `int(string, base)`
2. 10진수 -> 2, 8, 16진수: `bin()`, `oct()`, `hex()`
3. 10진수 -> n진수
   ```python
   def convert(num, base):
     temp = "0123456789ABCDEF"
     q, r = divmod(num, base)

     if q == 0:
        return temp[r]
     else:
        # q를 base로 변환
        # 즉, n진수의 다음 자리를 구함
        return convert(q, base) + temp[r]
   ```
4. `divmod(a, b)`: `a/b`의 몫과 나머지를 tuple 형태로 반환
