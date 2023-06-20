# `level 2` [3차] 압축
https://school.programmers.co.kr/learn/courses/30/lessons/17684

## 문제 설명

신입사원 어피치는 카카오톡으로 전송되는 메시지를 압축하여 전송 효율을 높이는 업무를 맡게 되었다. 메시지를 압축하더라도 전달되는 정보가 바뀌어서는 안 되므로, 압축 전의 정보를 완벽하게 복원 가능한 무손실 압축 알고리즘을 구현하기로 했다.

어피치는 여러 압축 알고리즘 중에서 성능이 좋고 구현이 간단한 LZW(Lempel–Ziv–Welch) 압축을 구현하기로 했다. LZW 압축은 1983년 발표된 알고리즘으로, 이미지 파일 포맷인 GIF 등 다양한 응용에서 사용되었다.

LZW 압축은 다음 과정을 거친다.

1. 길이가 1인 모든 단어를 포함하도록 사전을 초기화한다.
2. 사전에서 현재 입력과 일치하는 가장 긴 문자열 `w`를 찾는다.
3. `w`에 해당하는 사전의 색인 번호를 출력하고, 입력에서 `w`를 제거한다.
4. 입력에서 처리되지 않은 다음 글자가 남아있다면(`c`), `w+c`에 해당하는 단어를 사전에 등록한다.
5. 단계 2로 돌아간다.

압축 알고리즘이 영문 대문자만 처리한다고 할 때, 사전은 다음과 같이 초기화된다. 사전의 색인 번호는 정수값으로 주어지며, 1부터 시작한다고 하자.

![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/fb72051e-a76d-43f7-841c-740dc49efa87)

예를 들어 입력으로 `KAKAO`가 들어온다고 하자.

1. 현재 사전에는 `KAKAO`의 첫 글자 `K`는 등록되어 있으나, 두 번째 글자까지인 `KA`는 없으므로, 첫 글자 K에 해당하는 색인 번호 11을 출력하고, 다음 글자인 `A`를 포함한 `KA`를 사전에 27 번째로 등록한다.
2. 두 번째 글자 `A`는 사전에 있으나, 세 번째 글자까지인 `AK`는 사전에 없으므로, `A`의 색인 번호 1을 출력하고, `AK`를 사전에 28 번째로 등록한다.
3. 세 번째 글자에서 시작하는 `KA`가 사전에 있으므로, `KA`에 해당하는 색인 번호 27을 출력하고, 다음 글자 `O`를 포함한 `KAO`를 29 번째로 등록한다.
4. 마지막으로 처리되지 않은 글자 `O`에 해당하는 색인 번호 15를 출력한다.

![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/c6689c71-5378-4564-a5b6-0ef3b0a9a7b6)

이 과정을 거쳐 다섯 글자의 문장 KAKAO가 4개의 색인 번호 [11, 1, 27, 15]로 압축된다.

입력으로 `TOBEORNOTTOBEORTOBEORNOT`가 들어오면 다음과 같이 압축이 진행된다.

![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/30f53747-1e78-498e-b053-fd5b47fbdd03)

## 입력 형식
입력으로 영문 대문자로만 이뤄진 문자열 `msg`가 주어진다. `msg`의 길이는 1 글자 이상, 1000 글자 이하이다.

## 출력 형식
주어진 문자열을 압축한 후의 사전 색인 번호를 배열로 출력하라.

## 입출력 예제
![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/19725d2d-a9c3-4b61-83bd-2fa6e033ebae)

## My Solution

https://hazung.tistory.com/89 

Useful concept
- `chr(65)` 는 `A'를 출력한다.
  - 숫자가 기억나지 않는다면 `ord('A')`로 찾아볼 수 있다!
- list comprehension
- `break` 꼭 필요함: `while True` 로 했기 때문

```python
def solution(msg):
    d = {chr(65+i):1+i for i in range(26)}
    w = 0
    c = 0
    answer = []
    while True:
        c += 1
        if c == len(msg):
            answer.append(d[msg[w:c]])
            break  # 꼭 필요함!!
        if msg[w:c+1] not in d:
            answer.append(d[msg[w:c]])
            d[msg[w:c+1]] = len(d) + 1
            w = c
    return answer
```





