# `level 2` 피로도

## 문제 설명
XX게임에는 피로도 시스템(0 이상의 정수로 표현합니다)이 있으며, 일정 피로도를 사용해서 던전을 탐험할 수 있습니다. 이때, 각 던전마다 탐험을 시작하기 위해 필요한 "최소 필요 피로도"와 던전 탐험을 마쳤을 때 소모되는 "소모 피로도"가 있습니다. "최소 필요 피로도"는 해당 던전을 탐험하기 위해 가지고 있어야 하는 최소한의 피로도를 나타내며, "소모 피로도"는 던전을 탐험한 후 소모되는 피로도를 나타냅니다. 예를 들어 "최소 필요 피로도"가 80, "소모 피로도"가 20인 던전을 탐험하기 위해서는 유저의 현재 남은 피로도는 80 이상 이어야 하며, 던전을 탐험한 후에는 피로도 20이 소모됩니다.

이 게임에는 하루에 한 번씩 탐험할 수 있는 던전이 여러개 있는데, 한 유저가 오늘 이 던전들을 최대한 많이 탐험하려 합니다. 유저의 현재 피로도 k와 각 던전별 "최소 필요 피로도", "소모 피로도"가 담긴 2차원 배열 dungeons 가 매개변수로 주어질 때, 유저가 탐험할수 있는 최대 던전 수를 return 하도록 solution 함수를 완성해주세요.

## 제한사항
- k는 1 이상 5,000 이하인 자연수입니다.
- dungeons의 세로(행) 길이(즉, 던전의 개수)는 1 이상 8 이하입니다.
- dungeons의 가로(열) 길이는 2 입니다.
- dungeons의 각 행은 각 던전의 ["최소 필요 피로도", "소모 피로도"] 입니다.
- "최소 필요 피로도"는 항상 "소모 피로도"보다 크거나 같습니다.
- "최소 필요 피로도"와 "소모 피로도"는 1 이상 1,000 이하인 자연수입니다.
- 서로 다른 던전의 ["최소 필요 피로도", "소모 피로도"]가 서로 같을 수 있습니다.

## 입출력 예
![image](https://user-images.githubusercontent.com/122213470/230840491-fd130470-e559-4829-873c-58b07817d1ee.png)

## 주영's Solution

```python
from itertools import permutations   # 모든 순서를 찾는 문제

def solution(k, dungeons):
    result = []
    for p in permutations(dungeons, len(dungeons)):   # default는 전체 길이므로 len(dungeons) 빼도 됨
        # ([80, 20], [50, 40], [30, 10])
        cur = k   # 80 -> 60 -> 20
        cnt = 0   # 0 -> 1 -> 2
        
        
        for need, spend in p:
            if cur >= need:   # 20 < 30
                cur -= spend   # 60 -> 20
                cnt += 1   # 0 -> 1 -> 2
        result.append(cnt)
        
    return max(result)
```

## 서연's Solution

```python
from itertools import permutations
def solution(k, dungeons):
    answer = 0
    # 던전 경우의 수 생성 - 순열
    d = permutations(dungeons) # 디폴트가 전체 길이
    # 각 경우의수 별로
    # 현재 피로도 > 최소 피로도 이면,
    # 현재 - 소모
    # 탐험 던전 수 += 1
    for i in d: # 던전 탐험 경우의 수 i
        k_temp = k  # 각 경우의 수, 시작 피로도 리셋
        cnt = 0     # 각 경우의 수, 탐험 던전 수
        for need, loss in i: # 최소 피로도, 소모 피로도
            if k_temp >= need:
                k_temp -= loss
                cnt += 1
            else:
                break
        answer = max(answer, cnt)
    return answer
```

## 유경's Solution


## Useful Concepts
- `permutations`의 default = 전체 길이
