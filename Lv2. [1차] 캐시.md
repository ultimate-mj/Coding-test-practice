# `level 2` [1차] 캐시
(2018 KAKAO BLIND RECRUITMENT)
https://school.programmers.co.kr/learn/courses/30/lessons/17680

## 문제 설명
지도개발팀에서 근무하는 제이지는 지도에서 도시 이름을 검색하면 해당 도시와 관련된 맛집 게시물들을 데이터베이스에서 읽어 보여주는 서비스를 개발하고 있다.
이 프로그램의 테스팅 업무를 담당하고 있는 어피치는 서비스를 오픈하기 전 각 로직에 대한 성능 측정을 수행하였는데, 제이지가 작성한 부분 중 데이터베이스에서 게시물을 가져오는 부분의 실행시간이 너무 오래 걸린다는 것을 알게 되었다.
어피치는 제이지에게 해당 로직을 개선하라고 닦달하기 시작하였고, 제이지는 DB 캐시를 적용하여 성능 개선을 시도하고 있지만 캐시 크기를 얼마로 해야 효율적인지 몰라 난감한 상황이다.

어피치에게 시달리는 제이지를 도와, DB 캐시를 적용할 때 캐시 크기에 따른 실행시간 측정 프로그램을 작성하시오.

## 입력 형식
- 캐시 크기(cacheSize)와 도시이름 배열(cities)을 입력받는다.
- cacheSize는 정수이며, 범위는 0 ≦ cacheSize ≦ 30 이다.
- cities는 도시 이름으로 이뤄진 문자열 배열로, 최대 도시 수는 100,000개이다.
- 각 도시 이름은 공백, 숫자, 특수문자 등이 없는 영문자로 구성되며, 대소문자 구분을 하지 않는다. 도시 이름은 최대 20자로 이루어져 있다.

## 출력 형식
- 입력된 도시이름 배열을 순서대로 처리할 때, "총 실행시간"을 출력한다.

## 조건
- 캐시 교체 알고리즘은 LRU(Least Recently Used)를 사용한다.
- cache hit일 경우 실행시간은 1이다.
- cache miss일 경우 실행시간은 5이다.

## 입출력 예제
![image](https://github.com/ultimate-mj/Coding-test-practice/assets/122213470/e6ebaed5-82b8-48db-999e-bdc4c6d3b87c)

## Useful Concept
https://hanjo8813.github.io/programmers/19_2/
https://gengmi.tistory.com/entry/Cache-%EC%BA%90%EC%8B%9C-%EB%8F%99%EC%9E%91%EA%B3%BC-%EC%BA%90%EC%8B%9C-%EA%B5%90%EC%B2%B4-%EC%A0%95%EC%B1%85


- 캐시 교체 알고리즘: `Doubly Linked List` 또는 `Hash map` 으로 많이 구현
  - `FIFO(First in First Out)`: 가장 먼저 들어간 캐시를 교체
  - `LFU(Least Frequently Used)`: 사용 횟수가 가장 적은 캐시를 교체.
  - `LRU(Least Recently Used)`: 가장 오랫동안 사용되지 않은 것 교체 
- `cache hit`: CPU가 참조하고자 하는 메모리가 캐시에 존재하고 있을 경우
- `cache miss`: CPU가 참조하고자 하는 메모리가 캐시에 존재하지 않는 경우
- `cache size`: 저장할 수 있는 크기

## My Solution 1. 6개 중 4개 성공

Idea:
- `index` 를 조정하는 방법으로 `cacheSize` 조정

```python
ind = 0
ans = 0
left = 0

for i in range(len(cities)):
  if cities[ind] in cities[left:ind]:
    ans += 1
    cities.pop(ind)
  else:
    ans += 5
    ind += 1
  if ind - left > 3:
    left += 1
print(ans)
```

## My Solution 2. 20개 중 14개 성공

Idea:
- 대소문자 구별이 없음! use `capitalize`
  - use `list comprehension` 
- `pop`을 할 때 `ind`가 아니라 더 앞에 있는 것을 `pop`해야 함!
  - 여러 개의 값이 있을 경우, `index`는 가장 첫 번째만을 불러와서 이걸 사용!
- (어이없는 실수) `ind - left > 3` 이 아니라 `> cacheSize` 이어야 했음

```python
def solution(cacheSize, cities):
    cities = [i.capitalize() for i in cities]

    ind = 0
    ans = 0
    left = 0

    for i in range(len(cities)):
        if cities[ind] in cities[left:ind]:
            ans += 1
            cities.pop(cities.index(cities[ind]))
        else:
            ans += 5
            ind += 1
        if ind - left > cacheSize:
            left += 1
    return ans
```

## Other's Solution
https://velog.io/@tiiranocode/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%EC%BA%90%EC%8B%9C

나의 것과 비슷한데 나는 왜 틀렸는지 모르겠다...

Idea:
- use `lower()`
- use `pop` and `append`

```python
def solution(cacheSize, cities):
    cache = []
    time = 0
    for city in cities:
        city = city.lower()
        if cacheSize:
            if not city in cache:
                if len(cache) == cacheSize:
                    cache.pop(0)
                cache.append(city)
                time += 5
            else:
                cache.pop(cache.index(city))
                cache.append(city)
                time += 1
        else:
            time += 5
    return time
```

