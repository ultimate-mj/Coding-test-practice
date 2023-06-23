# `level 2` 전화번호 목록

## 문제 설명
전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.

- 구조대 : 119
- 박준영 : 97 674 223
- 지영석 : 11 9552 4421

전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.

## 제한 사항
- phone_book의 길이는 1 이상 1,000,000 이하입니다.
- 각 전화번호의 길이는 1 이상 20 이하입니다.
- 같은 전화번호가 중복해서 들어있지 않습니다.

## 입출력 예제
![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/6193184e-b869-4c52-b9d5-8c3106d489d4)

## My Solution. 정확성 100점, 효율성 2/4

Idea:
- 문자열로 이루어진 list는 원소 길이 기준으로 먼저 sorting 됨

```python
def solution(phone_book):
    phone_book.sort()  #원소의 길이를 기준으로 sort
    
    if len(phone_book) == 1:
        return True
    
    else:
        for i,x in enumerate(phone_book):  #가장 짧은 원소부터 기준으로
            for j in range(i+1, len(phone_book)):
                #if x in phone_book[j]:  #접두사와 같아야 함!!
                if x in phone_book[j][0:len(x)]:
                    return False
                
    answer = True
    return answer
```

## Other's Solution.

Idea:
- 문자열을 `sort`하면 길이로 정렬된 후 **문자열 기준으로도 정렬됨**
- use `zip`
  - ex) `list(zip([1,2,3], (4,5,6), "abcd"))` 의 결과는 `[[1, 4, 'a'], [2, 5, 'b'], [3, 6, 'c']]`
- use `A.startswith(B)`

```python
def solution(phone_book):
    phone_book.sort()  #원소의 길이를 기준으로 sort
    
    for p1, p2 in zip(phone_book, phone_book[1:]):
        if p2.startswith(p1):
            return False
    return True
```
