# 귤 고르기

## 문제 설명
경화는 과수원에서 귤을 수확했습니다. 경화는 수확한 귤 중 'k'개를 골라 상자 하나에 담아 판매하려고 합니다. 그런데 수확한 귤의 크기가 일정하지 않아 보기에 좋지 않다고 생각한 경화는 귤을 크기별로 분류했을 때 서로 다른 종류의 수를 최소화하고 싶습니다.

예를 들어, 경화가 수확한 귤 8개의 크기가 [1, 3, 2, 5, 4, 5, 2, 3] 이라고 합시다. 경화가 귤 6개를 판매하고 싶다면, 크기가 1, 4인 귤을 제외한 여섯 개의 귤을 상자에 담으면, 귤의 크기의 종류가 2, 3, 5로 총 3가지가 되며 이때가 서로 다른 종류가 최소일 때입니다.

경화가 한 상자에 담으려는 귤의 개수 k와 귤의 크기를 담은 배열 tangerine이 매개변수로 주어집니다. 경화가 귤 k개를 고를 때 크기가 서로 다른 종류의 수의 최솟값을 return 하도록 solution 함수를 작성해주세요.

## 제한사항
- 1 ≤ k ≤ tangerine의 길이 ≤ 100,000
- 1 ≤ tangerine의 원소 ≤ 10,000,000

## 입출력 예
![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/30a2dfb2-2120-43d1-aa52-4e017fb9c826)

## My Solution. 73.5점 (대부분 시간초과)

Idea:
- size와 그에 해당하는 개수를 `dictionary`로 만들자
  + size, count 리스트를 따로 만들어서 `zip`
  + 개수를 세는 `count` 함수 사용 -- 여기서 시간 초과 뜬 듯!!

주의:
- `dictionary`를 정렬할 때는 `sorted`사용
  + 이 때 `.items()`를 정렬해야 함
  + 정렬하고 나면 `tuple` 형태로 나옴

```python
def solution(k, tangerine):
    size = []
    count = []
    tangerine.sort()
    set_tangerine = list(set(tangerine)) # size 몇 종류 있는지
    
    loc = 0 #탐색 횟수 줄이기 위해
    for i, x in enumerate(set_tangerine):
        size.append(x)
        count.append(tangerine[loc:].count(x))
        loc += count[i]
        
    result = dict(zip(size, count)) #각 사이즈별로 몇 개 있는지를 dictionary 로
    result_sort = sorted(result.items(), key=lambda x:x[1], reverse = True) #개수가 많은 사이즈부터 sort
    
    box = 0
    counts = 0
    while counts < k:
        counts += result_sort[box][1]
        box += 1
    
    return box
```

## Other's Solution

https://velog.io/@minmong/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-Lv.2-%EA%B7%A4-%EA%B3%A0%EB%A5%B4%EA%B8%B0-Python-velog

Idea:
- `for`문 한 번만 돌려서 개수 세기

```python
def solution(k, tangerine):
    answer = 0
    a={}
    for i in tangerine:
        if i in a:
            a[i]+=1
        else:
            a[i]=1
    a = dict(sorted(a.items(), key=lambda x: x[1], reverse=True))
    for i in a:
        if k<=0:
            return answer
        k-=a[i]
        answer+=1
    return answer
```



