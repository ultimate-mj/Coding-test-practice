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

![image](https://user-images.githubusercontent.com/122213470/229417784-9edf25cf-e350-4742-9510-42145b4cfe71.png)

## My Solution

```python
def solution(phone_book):
    phone_book.sort(key = lambda x: len(x))  #원소의 길이를 기준으로 sort
    
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

![image](https://user-images.githubusercontent.com/122213470/229417830-ac17e948-9c90-4223-82cc-dbee6be55c2f.png)


## Other's Solution.

point:
- sort를 길이 기준이 아니라, 그냥 하기!!
  - 붙어있는 것끼리 가장 비슷할 것
+ You can also use `startswith`

```python
def solution(phone_book):
    # 한 원소 전체(j)가 다른 원소(i)의 앞부분에 i[:len(j)] 있어야함
    # 길이 순으로 정렬해서? 
    # 그냥 정렬하면 제일 비슷한게 서로 붙어있게 됨
    # for문 roop 돌리면서, i번째 원소와 i+1번째 원소를 비교
    p = phone_book.sort()
    j = None
    for i in phone_book:
        if j is not None and j==i[:len(j)]:
            return False
        # j는 이전 원소
        j = i
    return True
```

