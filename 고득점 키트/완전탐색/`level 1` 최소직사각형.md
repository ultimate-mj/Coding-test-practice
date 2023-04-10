# `level 1` 최소직사각형

## 문제 설명
명함 지갑을 만드는 회사에서 지갑의 크기를 정하려고 합니다. 다양한 모양과 크기의 명함들을 모두 수납할 수 있으면서, 작아서 들고 다니기 편한 지갑을 만들어야 합니다. 이러한 요건을 만족하는 지갑을 만들기 위해 디자인팀은 모든 명함의 가로 길이와 세로 길이를 조사했습니다.

아래 표는 4가지 명함의 가로 길이와 세로 길이를 나타냅니다.

![image](https://user-images.githubusercontent.com/122213470/230831841-9b6e3fb6-9d3a-4804-b6e0-694aafbf52f7.png)

가장 긴 가로 길이와 세로 길이가 각각 80, 70이기 때문에 80(가로) x 70(세로) 크기의 지갑을 만들면 모든 명함들을 수납할 수 있습니다. 하지만 2번 명함을 가로로 눕혀 수납한다면 80(가로) x 50(세로) 크기의 지갑으로 모든 명함들을 수납할 수 있습니다. 이때의 지갑 크기는 4000(=80 x 50)입니다.

모든 명함의 가로 길이와 세로 길이를 나타내는 2차원 배열 sizes가 매개변수로 주어집니다. 모든 명함을 수납할 수 있는 가장 작은 지갑을 만들 때, 지갑의 크기를 return 하도록 solution 함수를 완성해주세요.

## 제한사항
- sizes의 길이는 1 이상 10,000 이하입니다.
- sizes의 원소는 [w, h] 형식입니다.
- w는 명함의 가로 길이를 나타냅니다.
- h는 명함의 세로 길이를 나타냅니다.
- w와 h는 1 이상 1,000 이하인 자연수입니다.

## 입출력 예
![image](https://user-images.githubusercontent.com/122213470/230831937-88724bfe-faf8-4f8f-a7fd-05b7b0ec9709.png)


## My Solution

```python
def solution(sizes):
    w = []
    h = []
    for i in range(len(sizes)):
        if sizes[i][0] >= sizes[i][1]:
            w.append(sizes[i][0])
            h.append(sizes[i][1])
        else:
            w.append(sizes[i][1])
            h.append(sizes[i][0])
    answer = max(w)*max(h)
    return answer
```

## Other's Solution

https://velog.io/@guswl8280/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%EC%B5%9C%EC%86%8C-%EC%A7%81%EC%82%AC%EA%B0%81%ED%98%95-Python

```python
def solution(sizes):
    return max(max(x) for x in sizes) * max(min(x) for x in sizes)
```
