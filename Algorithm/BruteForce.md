### 알고리즘 패러다임
- 알고리즘 생각해내는 그 과정이 겹치는 경우가 있음, 접근법이 비슷한 것
- 자주 나타나는 알고리즘 접근법을 묶어서 알고리즘 패러다임이라고 함, 여러 가지 있을 수 있음

### Brute Force 소개
- 무차별적으로 가능한 모든 방법을 시도하는 것임
- 가능한 모든 경우의 수를 다 시도하는 것

### Brute Force 평가
- 가능한 모든 조합을 만듬, 모든 경우의 수를 구하지만 비효율적임
- 인풋이 커질수록 비효율이 매우 커짐
- 직관적이고 명확하고 코드를 작성하기 쉽고 답을 확실하게 찾을 수 있는 장점이 있긴함
- 인풋이 크지 않으면 그냥 사용해도 괜찮음
- 인풋이 엄청 큰 경우에는 Brute Force는 비효율적임
- 효율적인 알고리즘의 첫 시작은 Brute Force임, 거기서부터 시작해서 발전시켜나감

### 가까운 매장 찾기
- 튜플리스트로 매장들 좌표 위치를 받은 것을 바탕으로 두 좌표 사이 거리를 구한 뒤 가까운 매장을 찾는 문제
- 내 풀이
```python
# 제곱근 사용을 위한 sqrt 함수
from math import sqrt

# 두 매장의 직선 거리를 계산해 주는 함수
def distance(store1, store2):
    return sqrt((store1[0] - store2[0]) ** 2 + (store1[1] - store2[1]) ** 2)

# 가장 가까운 두 매장을 찾아주는 함수
def closest_pair(coordinates):
    # 여기 코드를 쓰세요
    min = 9999
    tmp = 0
    for i in range(len(coordinates) - 1):
        for j in range(i + 1, len(coordinates)):
            tmp = distance(coordinates[i], coordinates[j])
            if min > tmp:
                min = tmp
                idx1 = i
                idx2 = j
    return [coordinates[idx1], coordinates[idx2]]
# 테스트
test_coordinates = [(2, 3), (12, 30), (40, 50), (5, 1), (12, 10), (3, 4)]
print(closest_pair(test_coordinates))
```

- 풀이
- pair을 통해서 해당 튜플에 데이터를 받아서 계산을 하고, 입력 받은 튜플 데이터 값을 바탕으로 반복문을 통해서 Brute Force로 풀음
- 여기서 조합은 첫번째 페어부터 시작해서 하나씩 찾기 때문에 1-2 , 1-3, 1-4, 1-5, 2-3, 2-4, 2-5, 3-4, 3-5, 4-5 순으로 찾기 때문에 반복문을 i부터 시작해서 끝까지 훑어 보는것에서 j는 i다음인 수인 i+1부터 끝까지 탐색하는 것으로 해야 조합의 패턴을 맞춰서 확인을 할 수 있음
```python
# 제곱근 사용을 위한 sqrt 함수 불러오기
from math import sqrt

# 두 매장의 직선 거리를 계산해 주는 함수
def distance(store1, store2):
    return sqrt((store1[0] - store2[0]) ** 2 + (store1[1] - store2[1]) ** 2)

# 가장 가까운 두 매장을 찾아주는 함수
def closest_pair(coordinates):
    # 현재까지 본 가장 가까운 두 매장
    pair = [coordinates[0], coordinates[1]]
  
    for i in range(len(coordinates) - 1):
        for j in range(i + 1, len(coordinates)):
            store1, store2 = coordinates[i], coordinates[j]

            # 더 가까운 두 매장을 찾으면 pair 업데이트
            if distance(pair[0], pair[1]) > distance(store1, store2):
                pair = [store1, store2]

    return pair

# 테스트
test_coordinates = [(2, 3), (12, 30), (40, 50), (5, 1), (12, 10), (3, 4)]
print(closest_pair(test_coordinates))
```

### 강남역 폭우
- 건물과 건물 사이에 얼마만큼의 빗물이 담길 수 있는지 알고자 할 때 그것을 계산해주는 함수 작성
- 만일 [3,0,0,2,0,4]의 buildings이 들어오면 각각 인덱스의 건물의 높이를 말하는 것이고 그 사이에 빗물이 담길 수 있는 것은 외관상 10을 담을 수 있음 건물 사이 기준으로 빗물이 담기므로
- 풀이
- 각 인덱스에 담기는 빗물의 양을 계산해서 모두 더해줘야 하는데 이 빗물이 담기는 조건 중 0번 인덱스와 마지막은 빗물이 담길 수 없음
- 여기서 나머지 인덱스에서 빗물이 담기기 위해서는 더 큰 건물들 사이에 끼어 있으면 빗물이 담기는 것임, 그게 당장 내 위치기준 앞 뒤 인덱스가 아니라 왼쪽 오른쪽 기준으로 나보다 높은 건물이 있으면 빗물을 담을 수 있음
- 그렇기 때문에 현재 인덱스 기준으로 왼쪽에 있는 건물들 중 가장 높은 건물의 높이를 구하고 또 현재 인덱스 기준으로 오른쪽에 있는 건물들 중 가장 높은 건물의 높이를 구한뒤 그 중 더 낮은 건물의 높이를 구하고 그 높이에서 현재 인덱스에 있는 건물의 높이를 빼면 건물들 사이에서 빗물이 담길 수 있는 양이 나오게 됨
- 그림은 아래와 같음

![picture](/img/Alogorithm/BruteForce/one.png)

- 그렇기 때문에 위의 그림을 예시로 들면 첫번째와 마지막은 의미가 없어서 지나가고 1번 인덱스를 보면 높이가 1이고 1번 인덱스 기준 왼쪽 [:1], 1번 인덱스 기준 오른쪽 [1:]를 통해서 각각 높은 건물의 높이가 1, 3이 되는것을 알 수 있음
- 여기서 높은 건물들 사이에 끼어서 빗물을 받으므로 왼쪽 오른쪽 기준으로 그 중에서 더 낮은 건물의 높이를 구한다, 그래야 더 낮으니깐 빗물이 담기므로 그리고 그 기준을 바탕으로 현재 인덱스에 차감을 하는데 그렇게 되면 값은 upper_bound =1, 여기서 현재 인덱스를 빼면 0이다 그래서 담을 수가 없다
- 이를 2번 인덱스 기준으로 다시 계산을 해보면 2번 인덱스 기준으로 왼쪽 건물 중 높은 것의 높이는 1이고 오른쪽은 3인데 여기서도 빗물이 담길 수 있는 것은 그 사이에 껴서 담기는 것이므로 높으면 애초에 담긴다는 가정이 성립이 안되므로 더 작은 값을 찾으면 upper_bound가 1이고 현재 인덱스 기준으로 생각하면 현재 인덱스는 높이가 0이므로 1정도 높이의 빗물은 담길 수 있게 되는 것이다
- 사이에 껴서 담기는 로직을 생각해야한다
- 여기서 한 가지 더 즉 담기는 빗물의 양 계산을 할 때 봐야하는 것은 0과 비교해서 max 값을 확인해야하는 것이다 아예 안 담기면 0이 나오기 때문에 비교를 하는 것이다
```python
def trapping_rain(buildings):
    # 총 담기는 빗물의 양을 변수에 저장
    total_height = 0

    # 리스트의 각 인덱스을 돌면서 해당 칸에 담기는 빗물의 양을 구한다
    # 0번 인덱스와 마지막 인덱스는 볼 필요 없다
    for i in range(1, len(buildings) - 1):
        # 현재 인덱스를 기준으로 양쪽에 가장 높은 건물의 위치를 구한다
        max_left = max(buildings[:i])
        max_right = max(buildings[i:])

        # 현재 인덱스에 빗물이 담길 수 있는 높이
        upper_bound = min(max_left, max_right)

        # 현재 인덱스에 담기는 빗물의 양을 계산
        # 만약 upper_bound가 현재 인덱스 건물보다 높지 않다면, 현재 인덱스에 담기는 빗물은 0
        total_height += max(0, upper_bound - buildings[i])

    return total_height

# 테스트
print(trapping_rain([0, 3, 0, 0, 2, 0, 4]))
print(trapping_rain([0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]))
```