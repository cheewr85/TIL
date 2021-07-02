### 분할 정복
- 재귀적 개념을 기반으로 함
- 문제가 있다면 이를 부분 문제로 나눈뒤 부분문제에서 구한 답을 문제를 푸는데 해결함
- 3단계로 나뉨 1.Divide 2.Conquer 3.Combine

![picture](/img/Alogorithm/Divide/one.png)

- Conquer 단계를 생각할 때 이 부분에서 다시 Divide and Conquer로 나눠서 풀어야 하는 경우가 생길수 있음
- 이런식으로 문제가 충분히 작아질 때까지 계속 나눠야함
- Divide → 문제를 부분 문제로 나눈다 / Conquer → 각 부분 문제를 정복한다 / Combine → 부분 문제들의 솔루션을 합쳐서 기존 문제를 해결함
- 예시
- 1~100의 합
- 1~50의 합, 51~100의 합으로 나눌 수 있음, 여기서 1~50의 합을 구하고 51~100의 합을 구한 뒤 이 두 합을 더하면 1~100의 합을 구함
- 이를 더 세밀하게 나뉘어져서 계산이 됨, 재귀적으로 계산
- 1부터 n까지의 합
- 재귀적으로 풀기 위한 base case의 경우 34에서 34까지의 합은 그냥 그 값을 리턴하면 됨
- 그리고 Divide하기 위해서는 주어진 문제를 반으로 나누면 됨 그러면 딱 중간값으로 생각하고 mid를 나눔
- 그 다음 재귀적으로 구하는데 결과적으로 base case로 수렴하는 과정이기 때문에 주어진 기준점으로 재귀적으로 계속 더하는 구조로 하면 됨
- 예를 들어 1~10이면 나눌 때 1~5, 6~10으로 나뉘므로 이에 맞게 코드를 작성함


```python
def consecutive_sum(start, end):
    # 코드를 작성하세요
   
    if start == end:
        return start
        
    mid = (start + end) // 2
    
    return consecutive_sum(start, mid) + consecutive_sum(mid+1, end)

# 테스트
print(consecutive_sum(1, 10))
print(consecutive_sum(1, 100))
print(consecutive_sum(1, 253))
print(consecutive_sum(1, 388))
```

### 합병 정렬
- Divide & Conquer를 사용함
- 리스트를 반으로 나눔 → 왼쪽 리스트와 오른쪽 리스트를 각각 정렬함 → 정렬된 두 리스트를 하나의 정렬된 리스트로 합병함
- 가장 왼쪽에 있는값들끼리 비교해서 거기서 작은 값이 들어가게 합치면 됨
- merge 함수 작성
- merged_list라는 빈 리스트를 생성하여서 리스트들을 비교해서 가장 작은 값 먼저 넣어서 정렬을 하게끔 하고 리스트가 다 끝나면 나머지 값을 넣게끔 구현하면 됨
```python
def merge(list1, list2):
    # 코드를 작성하세요.
    merged_list = []
    
    i = 0
    j = 0
    
    while i < len(list1) and j < len(list2):
        if list1[i] > list2[j]:
            merged_list.append(list2[j])
            j += 1
        else:
            merged_list.append(list1[i])
            i += 1
    
    if i==len(list1):
            merged_list += list2[j:]
    if j==len(list2):
            merged_list += list1[i:]
    
    return merged_list
        
# 테스트
print(merge([1],[]))
print(merge([],[1]))
print(merge([2],[1]))
print(merge([1, 2, 3, 4],[5, 6, 7, 8]))
print(merge([5, 6, 7, 8],[1, 2, 3, 4]))
print(merge([4, 7, 8, 9],[1, 3, 6, 10]))
```

- 합병정렬
- base case 역시 더 이상 쪼개지지 않는 상황인데 길이가 0이거나 1일 때임
- 그리고 반씩 나누는 과정 역시 슬라이싱을 통해서 왼쪽, 오른쪽 절반씩 나누면 됨
- 여기서 재귀적으로 merge 함수를 활용하여서 왼쪽, 오른쪽 절반씩 나눈 것을 merge_sort 함수를 통해서 계속 나누고 합치는 과정을 merge 함수를 이용해서 하나씩 합치면 됨
```python
def merge(list1, list2):
    # 이전 과제에서 작성한 코드를 붙여 넣으세요!
    merged_list = []
    
    i = 0
    j = 0
    
    while i < len(list1) and j < len(list2):
        if list1[i] > list2[j]:
            merged_list.append(list2[j])
            j += 1
        else:
            merged_list.append(list1[i])
            i += 1
    
    if i==len(list1):
            merged_list += list2[j:]
    if j==len(list2):
            merged_list += list1[i:]
    
    return merged_list
# 합병 정렬
def merge_sort(my_list):
    # 코드를 입력하세요.
    if len(my_list) < 2:
        return my_list
    
    
    left_half = my_list[:len(my_list)//2]
    right_half = my_list[len(my_list)//2:]
    
    return merge(merge_sort(left_half),merge_sort(right_half))

# 테스트
print(merge_sort([1, 3, 5, 7, 9, 11, 13, 11]))
print(merge_sort([28, 13, 9, 30, 1, 48, 5, 7, 15]))
print(merge_sort([2, 5, 6, 7, 1, 2, 4, 7, 10, 11, 4, 15, 13, 1, 6, 4]))
```

### 퀵 정렬
- Divide and Conquer를 활용함
- 퀵 정렬은 Divide 부분에서 대부분의 일을 함
- 퀵 정렬은 Partition으로 리스트를 나눔, pivot 기준점을 기준으로 값들을 배치함, pivot보다 작은 값은 왼쪽으로 큰 값은 오른쪽으로 배치함
- Divide → pivot을 기준으로 Partition하는 과정, Conquer → Pivot 왼쪽과 오른쪽의 값들을 정렬을 해 줌
- 이 기준으로 Divide and Conquer가 계속해서 일어남
- partition 함수에서 리스트와 인덱스 start, end를 파라미터로 받아서 구분해야함, pivot 그룹과 pivot보다 작은 small 그룹, pivot보다 큰 그룹인 Big 그룹, 아직 모르는 그룹으로 나눔
- 마지막 값을 pivot으로 받을거임, big 그룹 시작되는 인덱스, 현재 보는 인덱스를 나눔
- 아래와 같이 하나씩 탐색하면서 인덱스를 가르키는 값을 다르게 하면서 구분을 함

![picture](/img/Alogorithm/Divide/two.png)

- Partition 구현
- 그룹별로 나눈 뒤 마지막에 pivot값만 해당 위치로 보내면 됨
```python
# 두 요소의 위치를 바꿔주는 helper function
def swap_elements(my_list, index1, index2):
    # 코드를 작성하세요.
    temp = my_list[index1]
    my_list[index1] = my_list[index2]
    my_list[index2] = temp

# 퀵 정렬에서 사용되는 partition 함수
def partition(my_list, start, end):
    # 코드를 작성하세요.
    # i,b,start 모두 첫번째 인덱스에서 시작
    # i는 시작 인덱스, b는 Big 그룹이 시작하는 인덱스를 뜻함
    # 즉 pivot 기준 큰 값의 인덱스가 b, i는 그냥 탐색하는 인덱스
    # start, end는 그냥 시작과 끝점
    i = start
    b = start
    # pivot 값은 마지막 인덱스로
    p = end
    
    # p는 마지막 값을 가르키므로 i는 p보다 클 수 없음
    while i < p:
        
        # 만일 Big 그룹에 속한다면 Big 그룹을 만들기 위해서 i와 b를 서로 스왑함
        # 스왑을 한 뒤 big그룹을 유지하기 위해서 인덱스를 더함 i도 더하고
        # 이러면 자연스럽게 b는 big그룹에 첫 인덱스를 가르키고 i는 탐색이고
        # pivot은 그대로 있고 나머지 그룹은 Small 그룹으로 분할됨
        if my_list[i] <= my_list[p]:
            swap_elements(my_list, i, b)
            b += 1
        # i는 계속해서 탐색하기 때문에 조건과 상관없이 계속 카운팅
        i += 1
    # 반복문으로 탐색을 다 끝낸 뒤 마지막에 b가 가르키는 인덱스 값과 pivot 값을 바꾼다면
    # pivot값 기준으로 왼쪽은 Small 그룹 오른쪽은 Big그룹으로 나뉘게 됨
    swap_elements(my_list, b, p)
    p = b
    
		# pivot의 최종 인덱스 리턴해줌
    return p
    
# 테스트 1
list1 = [4, 3, 6, 2, 7, 1, 5]
pivot_index1 = partition(list1, 0, len(list1) - 1)
print(list1)
print(pivot_index1)

# 테스트 2
list2 = [6, 1, 2, 6, 3, 5, 4]
pivot_index2 = partition(list2, 0, len(list2) - 1)
print(list2)
print(pivot_index2)
```

- 퀵 정렬 구현하기
- partition을 기준으로 pivot의 왼쪽과 오른쪽을 구분해서 quicksort를 진행하면 됨
```python
# 두 요소의 위치를 바꿔주는 helper function
def swap_elements(my_list, index1, index2):
    # 코드를 작성하세요.
    temp = my_list[index1]
    my_list[index1] = my_list[index2]
    my_list[index2] = temp

# 퀵 정렬에서 사용되는 partition 함수
def partition(my_list, start, end):
    # 코드를 작성하세요.
    # i,b,start 모두 첫번째 인덱스에서 시작
    # i는 시작 인덱스, b는 Big 그룹이 시작하는 인덱스를 뜻함
    # 즉 pivot 기준 큰 값의 인덱스가 b, i는 그냥 탐색하는 인덱스
    # start, end는 그냥 시작과 끝점
    i = start
    b = start
    # pivot 값은 마지막 인덱스로
    p = end
    
    # p는 마지막 값을 가르키므로 i는 p보다 클 수 없음
    while i < p:
        
        # 만일 Big 그룹에 속한다면 Big 그룹을 만들기 위해서 i와 b를 서로 스왑함
        # 스왑을 한 뒤 big그룹을 유지하기 위해서 인덱스를 더함 i도 더하고
        # 이러면 자연스럽게 b는 big그룹에 첫 인덱스를 가르키고 i는 탐색이고
        # pivot은 그대로 있고 나머지 그룹은 Small 그룹으로 분할됨
        if my_list[i] <= my_list[p]:
            swap_elements(my_list, i, b)
            b += 1
        # i는 계속해서 탐색하기 때문에 조건과 상관없이 계속 카운팅
        i += 1
    # 반복문으로 탐색을 다 끝낸 뒤 마지막에 b가 가르키는 인덱스 값과 pivot 값을 바꾼다면
    # pivot값 기준으로 왼쪽은 Small 그룹 오른쪽은 Big그룹으로 나뉘게 됨
    swap_elements(my_list, b, p)
    p = b
    
    return p

    
# 퀵 정렬
def quicksort(my_list, start, end):
    # 코드를 작성하세요.
    if end - start < 1:
        return
    
		# pivot 값을 받음
    pivot = partition(my_list, start, end)
    # pivot 기준 왼쪽 Small 그룹
    quicksort(my_list, start, pivot - 1)
    # pivot 기준 오른쪽 Big 그룹
    quicksort(my_list, pivot + 1, end)
    
    

# 테스트 1
list1 = [1, 3, 5, 7, 9, 11, 13, 11]
quicksort(list1, 0, len(list1) - 1)
print(list1)

# 테스트 2
list2 = [28, 13, 9, 30, 1, 48, 5, 7, 15]
quicksort(list2, 0, len(list2) - 1)
print(list2)

# 테스트 3
list3 = [2, 5, 6, 7, 1, 2, 4, 7, 10, 11, 4, 15, 13, 1, 6, 4]
quicksort(list3, 0, len(list3) - 1)
print(list3)
```

- 옵셔널 파라미터를 활용하여 quicksort 줄이기
```python
# 두 요소의 위치를 바꿔주는 helper function
def swap_elements(my_list, index1, index2):
    # 코드를 작성하세요.
    temp = my_list[index1]
    my_list[index1] = my_list[index2]
    my_list[index2] = temp

# 퀵 정렬에서 사용되는 partition 함수
def partition(my_list, start, end):
    # 코드를 작성하세요.
    # i,b,start 모두 첫번째 인덱스에서 시작
    # i는 시작 인덱스, b는 Big 그룹이 시작하는 인덱스를 뜻함
    # 즉 pivot 기준 큰 값의 인덱스가 b, i는 그냥 탐색하는 인덱스
    # start, end는 그냥 시작과 끝점
    i = start
    b = start
    # pivot 값은 마지막 인덱스로
    p = end
    
    # p는 마지막 값을 가르키므로 i는 p보다 클 수 없음
    while i < p:
        
        # 만일 Big 그룹에 속한다면 Big 그룹을 만들기 위해서 i와 b를 서로 스왑함
        # 스왑을 한 뒤 big그룹을 유지하기 위해서 인덱스를 더함 i도 더하고
        # 이러면 자연스럽게 b는 big그룹에 첫 인덱스를 가르키고 i는 탐색이고
        # pivot은 그대로 있고 나머지 그룹은 Small 그룹으로 분할됨
        if my_list[i] <= my_list[p]:
            swap_elements(my_list, i, b)
            b += 1
        # i는 계속해서 탐색하기 때문에 조건과 상관없이 계속 카운팅
        i += 1
    # 반복문으로 탐색을 다 끝낸 뒤 마지막에 b가 가르키는 인덱스 값과 pivot 값을 바꾼다면
    # pivot값 기준으로 왼쪽은 Small 그룹 오른쪽은 Big그룹으로 나뉘게 됨
    swap_elements(my_list, b, p)
    p = b
    
    return p

    
# 퀵 정렬
def quicksort(my_list, start=0, end=None):
    # 코드를 작성하세요.
    if end == None:
        end = len(my_list) - 1
    
    if end - start < 1:
        return
    
		# pivot 값을 받음
    pivot = partition(my_list, start, end)
    # pivot 기준 왼쪽 Small 그룹
    quicksort(my_list, start, pivot - 1)
    # pivot 기준 오른쪽 Big 그룹
    quicksort(my_list, pivot + 1, end)
    
    

# 테스트 1
list1 = [1, 3, 5, 7, 9, 11, 13, 11]
quicksort(list1)
print(list1)

# 테스트 2
list2 = [28, 13, 9, 30, 1, 48, 5, 7, 15]
quicksort(list2)
print(list2)

# 테스트 3
list3 = [2, 5, 6, 7, 1, 2, 4, 7, 10, 11, 4, 15, 13, 1, 6, 4]
quicksort(list3)
print(list3)
```