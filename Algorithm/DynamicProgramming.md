### 최적 부분 구조(Optimal Substructure)
- 부분 문제들의 최적의 답을 이용해서 기존 문제의 최적의 답을 구할 수 있다는 것
- fib(5)를 구하기 위해서 fib(4)와 fib(3)의 값을 구한 뒤 그 값을 더해서 fib(5)의 값을 구함
- 이것이 최적 부분 구조임
- 이것은 최단 경로 찾기에도 해당될 수 있음

### 중복되는 부분 문제(Overlapping Subproblem)
- 중복으로 계산을 하는 부분이 존재함
- 중복되는 부분 문제를 여러번 계산하는 것은 비효율적임

### Dynamic Programming
- 최적 부분 구조가 있다 → 기존 문제를 부분 문제로 나눠서 풀 수 있음 → 중복되는 부분 문제들이 있음
- 이러한 구조를 해결하는 것이 Dynamic Programming을 통해서 해결할 수 있음
- Dynamic Programming은 한 번 계산한 결과를 재활용하는 방식임
- 중복되는 문제를 계속 다시 푸는게 아니라 한 번만 풀고 기억해두는 것
- 중복되는 문제를 한 번만 푸는 것이 목적
- Dynamic Programming은 Memoization과 Tabulation으로 나뉨

### Memoization
- 중복되는 계산은 한 번만 계산 후 메모
- 한 번 계산한 값을 저장해두는 것을 Cache로 상정하고 아래와 같이 피보나치 수를 Memoization으로 연산할 수 있음
- 아래와 같이 결과값을 캐시에 저장해두고 이를 필요할 때 캐시에서 가져다 쓰는 것임
- 각 부분 문제를 딱 한 번씩만 품, 중복의 비효율성 해결
- 이를 Top-down Approach 하향식 접근이라고 함

![picture](/img/Alogorithm/Dynamic/one.png)

- 코드는 아래와 같이 됨
- 사전 형식을 사용함, 위와 같은 트리 형태로 가지를 뻗은 후 계산을 한 것을 사전에 Cache로 저장함
```python
def fib_memo(n, cache):
    # 코드를 작성하세요.
		# base case
    if n < 3:
        return 1
    
		# 사전 형식을 썼기 때문에 n이라는 key 즉 n번째 피보나치를 계산했으면
		# 저장된 값을 리턴함
		# 3 : 2에 저장되었다면 3 in cache -> 3 존재함(key로) -> cache[3] = 2 리턴
    if n in cache:
        return cache[n]
    
		# 만일 저장되어 있지 않다면 피보나치 개념을 적용해서 직접 계산후
		# 사전식으로 저장 cahce[n] = 값 -> n번째 피보나치수
    cache[n] = fib_memo(n-1, cache) + fib_memo(n-2, cache)
    
		# 계산한 값 리턴함
    return cache[n]

def fib(n):
    # n번째 피보나치 수를 담는 사전
    fib_cache = {}

    return fib_memo(n, fib_cache)

# 테스트
print(fib(10))
print(fib(50))
print(fib(100))
```

### Tabulation
- 중복되는 것부터 풀음
- 아래에서 위로 올라가는 방식

![picture](/img/Alogorithm/Dynamic/two.png)

- 이런 방식은 상향식 접근 Bottom-Up Approach라고 함
- 표를 채워나가는 느낌임 아래와 같이(Table 방식으로 정리)

![picture](/img/Alogorithm/Dynamic/three.png)

- Memoization은 재귀를 기반으로 코드를 작성하고 Tabulation을 반복문을 통해서 리스트를 채워감
- 코드
- 단순하게 반복문을 사용하므로 기본 수를 리스트로 선언한 뒤 그 합을 append로 추가하면 됨, 그리고 마지막 인덱스가 구하고자 하는 결과값이 됨
```python
def fib_tab(n):
    # 코드를 작성하세요.
    fib_table = [0, 1, 1]
    
    for i in range(3, n+1):
        fib_table.append(fib_table[i-1] + fib_table[i-2])
        
        
    return fib_table[n]
# 테스트
print(fib_tab(10))
print(fib_tab(56))
print(fib_tab(132))
```

### Memoization vs Tabulation
- 둘의 공통점은 중복되는 부분 문제의 비효율을 해결해주는 점이 있음
- 가장 큰 차이점은 Memoization은 재귀함수를 사용하고 Tabulation은 반복문을 사용함
- 재귀호출이 계속 일어나면 스택이 쌓이고 오류가 날 수 있음
- 반복문은 그럴 위험은 없으나 n번쨰 값을 위해 모두 계산함, 중간에 필요없는 것들까지 계산하게 될 수도 있음
- Memoization은 필요한 계산을 뭔지 요구하는 거라 필요없는 계산은 안해도 됨

### Dynamic Programming 공간 최적화
- 피보나치 수열을 Tabulation으로 사용하면 O(n)이 시간복잡도, 공간복잡도가 됨
- 더 효율적으로 하기위해서 리스트 대신 가장 최근 값들을 저장하는 변수 두 개를 사용하면 됨
- 가장 최근 값을 나타내는 current와 그 직전 값을 나타내는 previous를 이용해서 두 값을 업데이트 하면서 관리할 수 있음

![picture](/img/Alogorithm/Dynamic/four.png)

- 사용하는 메모리는 고정되어 있기 때문에 공간복잡도는 O(1)임
- Dynamic Programming을 할 때, 모든 계산값을 저장할 필요가 없다면, 공간 사용을 최적화하면 좋음
- 반복문을 활용해서 해당 인덱스 값까지 피보나치 계산을 하면 됨
- current와 previous를 미리 선언하고 초기화 한 뒤 반복문으로 계산을 함

```python
def fib_optimized(n):
    # 코드를 작성하세요. 
    current = 1
    previous = 0
    
    for i in range(1, n):
        tmp = current
        current = previous + current
        previous = tmp
    
    return current
    
# 테스트
print(fib_optimized(16))
print(fib_optimized(53))
print(fib_optimized(213))
```

### 새꼼달꼼 장사
- 새꼼달꼼 장사를 할 때 갖고 있는 새꼼달꼼으로 벌어들일 수 있는 최대 수익은?
- price_list → 개수별 가격이 정리되어 있는 리스트
- count → 판매할 새꼼달꼼 개수
- cache → 개수별 최대 수익이 저장되어 있는 사전
- price_list = [0, 100, 400, 800, 900, 1000]이라면 새꼼달꼼 0개에 0원, 새꼼달꼼 1개에 100원, 새꼼달꼼 2개에 400원 등 가격이 책정됨
- 먼저 count는 최대 수익을 내려고 하는 것이기 때문에 0개나 1개인 경우 나눌 필요없이 그 가격만 하면 되니깐 Base case에 해당함, 이미 계산한 값은 cache에 리턴함 → Memoization이므로
- profit은 count개를 팔아서 가능한 최대수익을 저장하는 변수인데 우선 초기값 설정은 price_list에 있는 개수에 맞게 설정함, 없다면 0으로 상정
- count를 계산하기 위한 조합으로 2개인 경우는 2개와 1 + 1인 경우, 3개인 경우는 3개인 경우와 2 + 1 인 경우 4개인 경우는 4개와 3 + 1, 2 + 2인 경우로 나눌 수 있음
- 이를 반복문으로 구현함
- 그리고 계산된 profit의 값은 Cache에 사전형태로 저장함
```python
def max_profit_memo(price_list, count, cache):
    # Base Case: 0개 혹은 1개면 부분 문제로 나눌 필요가 없기 때문에 가격을 바로 리턴한다
    if count < 2:
        cache[count] = price_list[count]
        return price_list[count]

    # 이미 계산한 값이면 cache에 저장된 값을 리턴한다
    if count in cache:
        return cache[count]

    # profit은 count개를 팔아서 가능한 최대 수익을 저장하는 변수
    # 팔려고 하는 총개수에 대한 가격이 price_list에 없으면 일단 0으로 설정
    # 팔려고 하는 총개수에 대한 가격이 price_list에 있으면 일단 그 가격으로 설정
    if count < len(price_list):
        profit = price_list[count]
    else:
        profit = 0

    # count개를 팔 수 있는 조합들을 비교해서, 가능한 최대 수익을 profit에 저장
    for i in range(1, count // 2 + 1):
        profit = max(profit, max_profit_memo(price_list, i, cache) 
                 + max_profit_memo(price_list, count - i, cache))

    # 계산된 최대 수익을 cache에 저장
    cache[count] = profit

    return profit

def max_profit(price_list, count):
    max_profit_cache = {}

    return max_profit_memo(price_list, count, max_profit_cache)

# 테스트
print(max_profit([0, 100, 400, 800, 900, 1000], 5))
print(max_profit([0, 100, 400, 800, 900, 1000], 10))
print(max_profit([0, 100, 400, 800, 900, 1000, 1400, 1600, 2100, 2200], 9))
```

### Tabulation 방식
- 비슷한 로직을 반복문을 활용해서 이용할 수 있음
```python
def max_profit(price_list, count):
    # 코드를 작성하세요. 
    profit_table = [0]
    
    for i in range(1, count + 1):
        
        if i < len(price_list):
            profit = price_list[i]
        else:
            profit = 0
        
        for j in range(1, i // 2 + 1):
            profit = max(profit, profit_table[j] + profit_table[i - j])
        
        profit_table.append(profit)
        
    return profit_table[count]
    
# 테스트
print(max_profit([0, 200, 600, 900, 1200, 2000], 5))
print(max_profit([0, 300, 600, 700, 1100, 1400], 8))
print(max_profit([0, 100, 200, 400, 600, 900, 1200, 1300, 1500, 1800], 9))
```