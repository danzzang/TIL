[TOC]

# Data Structure

## 1. Array 🆚 Linked List 

![Linked List vs. Array | Studytonight](https://www.studytonight.com/data-structures/images/array-vs-linked-list.png)

### 1. Array

> 가장 기본적인 자료구조, 논리적 저장 순서와 물리적 저장 순서가 일치한다
>
> 따라서 인덱스로 해당 원소에 접근 할 수 있음. 그렇기 때문에 찾고자 하는 원소의 인덱스 값을 알고 있으면 `Big-O(1)`에 해당 원소로 접근 가능
>
> **random access** 가 가능하다는 장점 

> 하지만 삭제 또는 삽입의 과정에서는 해당 원소에 접근하여 작업을 완료한 뒤 => O(1)
>
> 추가적 작업이 필요하다.
>
> 예를 들면, 배열의 원소 중 한 가지를 삭제하면, 배열의 연속적인 특징이 깨지게 되고, 빈 공간이 생김 
>
> 삭제한 원소보다 큰 인덱스를 갖는 원소들은 shift 해주어야 하는 비용 발생, 이 경우 시간 복잡도는 O(n)
>
> Array 자료구조에서 삽입, 삭제 기능에 대한 time complexity의 worst case는 O(n)



### 2. Linked List

> 위의 문제를 해결하기 위한 자료 구조
>
> 각각의 원소들은 자기 자신 다음에 어떤 원소가 있는지만을 기억한다.
>
> 따라서 이 부분만 다른 값으로 바꿔주면 삭제와 삽입을 O(1)에 해결 가능

> 하지만 원하는 위치에 삽입을 할 때는 원하는 위치를 검색하는 과정에서 첫 번째부터 다 확인해야 함, Array와는 다르게 논리적 저장 순서와 물리적 저장 순서가 일치하지 않기 때문이다.
>
> 그래서 그 원소를 찾기 위해 시간 복잡도 O(n) 추가적으로 발생 

> Linked List는 Tree 구조의 근간이 되는 자료 구조, Tree에서 사용되었을 때 그 유용성이 드러남 



## 2. Stack & Queue

### 1. Stack

> 선형 자료구조, **Last In First Out (LIFO)**. 나중에 들어간 원소가 먼저 나온다.



### 2. Queue

> 선형 자료구조, **First In First Out (FIFO)**. 먼저 들어간 원소가 먼저 나온다.



![image-20201207140009122](file:///Users/leedain/Desktop/TIL/DB.assets/image-20201207140009122.png?lastModify=1608269609)



## 3. Tree

> 비선형 자료구조 , 계층적 관계(Hierarchical Relationship)를 표현하는 자료 구조 



### 1. 트리 구성요소

- **Node** : 트리를 구성하고 있는 각각의 요소 
- **Edge** : 트리를 구성하기 위해 노드와 노드를 연결하는 선 
- **Root Node** : 트리 구조에서 최상위에 있는 노드
- **Terminal Node (= leaf Node)** : 하위에 다른 노드가 연결되어 있지 않은 노드 의미
- **Internal Node** : leaf node를 제외한 모든 노드, root node도 포함



### 2. Binary Tree (이진트리)

> 루트 노드를 중심으로 두개의 서브 트리로 나뉘어 진다. 또한 나뉘어진 두 서브 트리도 모두 이진 트리어야 한다. 
>
> 공집합도 이진 트리로 포함시켜야 한다. 그래야 재귀적으로 조건을 확인해갔을 때, leaf node에 다달았을 때, 정의를 만족하기 때문이다. 따라서 노드가 하나 뿐인 것도 이진 트리 정의에 만족

![Binary tree - Wikipedia](https://upload.wikimedia.org/wikipedia/commons/f/f7/Binary_tree.svg)



> **Level**(레벨) : 각 층별, 루트 노드의 레벨은 0
>
> **height**(높이) : 트리의 최고 레벨, 위의 트리는 3레벨 ?



### 3. Perfect Binary Tree (포화 이진 트리) & Complete Binary Tree (완전 이진 트리)

![img](https://t1.daumcdn.net/cfile/tistory/992164335A05B1E21E)

> **포화 이진 트리** : 모든 레벨이 꽉 찬 이진 트리
>
> **완전 이진 트리** : 위에서 아래로, 왼쪽에서 오른쪽으로 순서대로 차곡차곡 채워진 이진 트리 

> 배열로 구성된 Binary Tree는 노드의 개수가 n개, root가 0이 아닌 1에서 시작할 때, 
>
> i 번째 노드에 대해서 parent(i) = i / 2, left_child(i) = 2i, right _child(i) = 2i + 1 의 index 값을 갖는다. 



### 4 . BST (Binary Search Tree)

> 이진 탐색 트리는 이진 트리의 일종 
>
> 이진 탐색 트리는 데이터를 저장하는 규칙이 있고, 규칙으로 특정 데이터의 위치를 찾는데 사용할 수 있다.

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/da/Binary_search_tree.svg/1200px-Binary_search_tree.svg.png" alt="Binary search tree - Wikipedia" style="zoom:33%;" />

**규칙**

1. **이진 탐색 트리의 노드에 저장된 키는 유일**
2. **부모의 키가 왼쪽 자식 노드의 키보다 크다**
3. **부모의 키가 오른쪽 자식 노드의 키보다 작다**
4. **왼쪽과 오른쪽 서브트리도 이진 탐색 트리이다**



> 이진 탐색 트리의 탐색 연산은 O(log n)의 시간 복잡도 가짐 
>
> 정확히 말하면 O(h) 라고 표현하는 것이 맞음
>
> 트리의 높이를 하나씩 더해갈수록 추가할 수 있는 노드의 수가 두 배씩 증가하기 때문
>
> 이러한 이진 탐색 트리는 Skewed Tree(편향 트리)가 될 수 있음, 저장 순서에 따라 계속 한 쪽으로만 노드가 추가되는 경우가 발생하기 때문이다. 이럴 경우 성능에 영향을 미치게 되며, 탐색의 Worst Case가 되고 시간 복잡도는 O(n)



### 5. Binary Heap

> 자료구조의 일종, Tree 형식을 하고 있으며, 배열에 기반한  Complete Binary Tree 
>
> 배열에 트리의 값들을 넣어줄 때, 0번 째는 건너 뛰고 **1번 index 부터 루트노드**가 시작됨 
>
> 노드의 고유번호 값과 배열의 index를 일치시켜 혼동을 줄이기 위함 

<img src="https://www.geeksforgeeks.org/wp-content/uploads/MinHeapAndMaxHeap.png" alt="Heap Data Structure - GeeksforGeeks" style="zoom:33%;" />

#### 1) Max Heap

> Root node에 있는 값이 제일 큼, 최댓값을 찾는데 소요되는 연산의 time complexity가 O(1)
>
> complete binary tree이기 때문에 배열을 사용하여 효율적으로 관리할 수 잇음 
>
> random access가 가능
>
> heap의 구조를 계속 유지하기 위해 제거된 루트 노드를 대체 할 다른 노드가 필요
>
> heap은 맨 마지막 노드를 루트 노드로 대체 시킨 후, 다시 heapify 과정을 거쳐 heap 구조 유지
>
> 이런 경우에는 결국 O(log n)의 시간복잡도고 최대값 또는 최소값에 접근



#### 2) Min Heap 

> Root node에 있는 값이 제일 작음, 최댓값을 찾는데 소요되는 연산의 time complexity가 O(1)
> max heap과 비슷



### 6. Red Black Tree

> RBT는 BST를 기반으로 하는 트리 형식의 자료 구조

> Search, Insert, Delete에 O(log n)의 시간 복잡도 소요 됨
>
> 동일한 노드 개수일 때, depth를 최소화하여 시간 복잡도를 줄이는 것이 핵심 
>
> 동일한 노드 개수일 때, drpth가 최소가 되는 경우 tree가 complete binary tree인 경우
![Red–black tree - Wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/6/66/Red-black_tree_example.svg/500px-Red-black_tree_example.svg.png)



#### 1) Red-Black Tree의 정의

> 1) 각 노드는 **Red** or **Black**의 색깔을 가짐
>
> 2) Root node의 색깔은 **Black**
>
> 3) 각 leaf node는 **Black**
>
> 4) 어떤 노드의 색깔이 **Red**라면 두 개의 Children의 색깔은 모두 **Black**
>
> 5) 각 노드에 대해서 노드로부터 descendant leaves 까지의 단순 경로는 모두 같은 수의 black nodes 들을 포함하고 있다. 이를 해당 노드의 `Black-Height`라고 한다.
>
> > **Black-Height**: 노드 x 로부터 노드 x 를 포함하지 않은 leaf node 까지의 simple path 상에 있는 black nodes 들의 개수_



#### 2) Red-Black Tree의 특징
> 1) Binary Search Tree 이므로 BST의 특징을 모두 가짐
>
> 2) Root node부터 leaf node 까지의 모든 경로 중 최소 경로와 최대 경로의 크기 비율은 2보다 크지 않음. 이러한 상태를 **balanced** 상태 
>
> 3) node의 child가 없을 경우 child를 가리키는 포인터는 NIL값 저장, 이러한 NIL 들을 leaf node로 간주



## 6. Hash Table

> Hash는 내부적으로 배열을 사용, 데이터를 저장하기 때문에 빠른 검색 속도
>
> 특정 값을 Search하는데 **데이터 고유의 인덱스**로 접근 => 인덱스가 해시 값? 
>
> average case에 대해 time complexity가 **O(1)**이 된다. 
>
> 특별한 알고리즘을 이용, 저장할 데이터와 연관된 고유한 숫자를 만들어 낸 뒤 이를 인덱스로 사용
>
> 특정 데이터가 저장되는 인덱스는 그 데이터만의 고유한 위치, 삽입 연산 시 다른 데이터의 사이에 끼어들거나, 삭제 시 다른 데이터로 채울 필요가 없으므로 연산에 추가적인 비용이 없도록 만들어짐 



### 1. Hash Function

> 특별한 알고리즘 => `hash method` , `hash function` 
>
> 이 메소드에 의해 변환된 데이터의 고유 숫자 값 => `hash code`
> 저장되는 값들의 key 값을 hash function을 통해서 작은 범위의 값들로 바꿔준다

> **collision** : 서로 다른 두 개의 키가 같은 인덱스로 hashing되면 같은 곳에 저장할 수 없게 됨 
>
> 어설픈 hash function을 통해서 key 값들을 결정하면 동일한 값이 도출될 수 있다.
>
> 이렇게 되면 동일한 key 값에 복수 개의 데이터가 하나의 테이블에 존재할 수 있게 되는데, 이를 collision 이라고 한다.




### 2.  collision 해결 방법 
> hashing 된 인덱스에 이미 다른 값이 있다면 새 데이터를 저장할 다른 위치를 찾은 뒤 저장해야 함. 
> 따라서 충돌 해결은 필수 !! 



#### 1) Open Address 방식 (개방주소법)
> 해시 충돌이 발생하면, (즉, 삽입하려는 해시 버킷이 이미 사용 중인 경우) **다른 해시 버킷에 해당 자료를 삽입하는 방식**
> 
> ** 버킷이란 데이터를 저장하기 위한 공간



1. **Linear Probing**
    
- 순차적으로 탐색하며 비어있는 버킷을 찾을 때까지 계속 진행
    
2. **Quadratic Probing**
    
- 2차 함수를 이용해 탐색할 위치 찾음
    
3. **Double hashing Probing**

    - 하나의 해쉬 함수에서 충돌이 발생하면 2차 해쉬 함수를 이용해 새로운 주소 할당 

    - 위의 2 가지 방법에 비해 많은 연산량 요구 
    - 

> ** Worst Case의 경우 비어있는 버킷을 찾지 못하고 탐색을 시작한 위치까지 되돌아 올 수 있음 



#### 2) Separate Chaining 방식 (분리연결법)
> Separate Chaining 방식은 해시 충돌이 잘 발생하지 않도록 보조 해시 함수를 통해 조정할 수 있다면, Worst Case에 가까워지는 빈도를 줄일 수 있음 



1. **연결 리스트를 사용하는 방식 (Linked List)**
- 각각의 버킷들을 연결리스트로 만들어 collision이 발생하면 해당 버킷의 리스트에 추가
- 연결 리스트의 특징을 그대로 이어받아 삭제 또는 삽입이 간단
- 하지만 작은 데이터들을 저장할 때 연결 리스트 자체의 오버헤드 부담 
- 버킷을 계속해서 사용하는 open address 방식에 비해 테이블 확장 늦출 수 있음



2. **Tree를 사용하는 방식 (Red-Black Tree)**
- 트리를 사용하는 방식
- 연결 리스트를 사용할 것인지 트리를 사용할 것인지에 대한 기준은 하나의 해시 버킷에 할당된 key-value 쌍의 개수
- 데이터 개수가 적다면 연결 리스트, 트리는 기본적으로 메모리 사용량이 많기 때문



### 3. 해시 버킷 동적 확장 (Resize)
> 해시 버킷 개수가 적다면 메모리 사용을 아낄 수 있지만, 해시 충돌로 인해 성능 상 손실이 발생
>
> 그래서 HashMap은 key-value 쌍 데이터 개수가 일정 개수 이상이 되면 해시 버킷의 개수를 두 배로 늘린다.  이렇게 늘리면 해시 충돌로 인한 성능 손실 문제를 어느 정도 해결 할 수 있음. 