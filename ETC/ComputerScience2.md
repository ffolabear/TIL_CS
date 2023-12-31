# CS 기초 관련 면접대비 질문 리스트 - 2

---

### 📄 Contents
> 실제 면접에서 나올법한 흐름으로 작성
- [1. List 에 대해 설명해주세요.](#1-list-에-대해-설명해주세요)
- [2. Stack 에 대해 설명헤 주세요.](#2-stack-에-대해-설명헤-주세요)
- [3. Queue 에 대해 설명헤 주세요.](#3-queue-에-대해-설명헤-주세요)
- [4. Deque 에 대해 설명헤 주세요.](#4-deque-에-대해-설명헤-주세요)
- [5. HashMap 에 대해 설명헤 주세요.](#5-hashmap-에-대해-설명헤-주세요)
- [6. Heap 에 대해 설명헤 주세요.](#6-heap-에-대해-설명헤-주세요)
- [7. BST 에 대해 설명헤 주세요.](#7-bst-에-대해-설명헤-주세요)

---

### 1. List 에 대해 설명해주세요.
- 데이터가 연속적으로 연결되어 있는 선형 자료구조
- i번 인덱스에 접근 : `O(1)`
- 탐색 : `O(N)`
- 추가
  - 리스트의 끝에 : `Amortized O(1)`
  - 그 외에 : `O(N)`


<details>
<summary>꼬리질문</summary>
<div markdown="1">

### LinkedList 와 어떤것이 다른지 설명해 주세요.
- 메모리 상에서 데이터가 불연속적으로 저장
- 여러개의 노드(Node) 들로 이루어져 있으며 하나의 노드는 값(value) 와 다음 노드의 주소(메모리 주소)를 쌍으로 가지고 있음
- List 와 다르게 데이터 추가는 `O(1)`, 탐색은 `O(N)`
- 검색보다 삽입 삭제가 빈번한 경우에 적합


</div>
</details>

<br>

[⬆️ 처음으로](#-contents)

### 2. Stack 에 대해 설명헤 주세요.
- 데이터가 연속적(논리적)으로 연결되어 있는 선형 자료구조
- LIFO
- i번째 데이터에 접근 : `O(N)`
- 맨 위(뒤) 데이터에 접근/삭제 : `O(1)`
- 탐색 : `O(N)`


<br>

[⬆️ 처음으로](#-contents)

### 3. Queue 에 대해 설명헤 주세요.
- 데이터가 연속적(논리적)으로 저장되어 있는 선형 자료구조
- FIFO
- i번째 데이터에 접근 : `O(N)`
- 맨 앞 데이터에 접근/삭제 : `O(1)`
- 맨 뒤에 데이터 추가 : `O(1)`
- 탐색 : `O(N)`

<br>

[⬆️ 처음으로](#-contents)

### 4. Deque 에 대해 설명헤 주세요.
- 한 방향으로만 데이터를 넣거나 꺼내는게 아니라 양쪽 끝에서 데이터를 추가 하거나 꺼낼수 있는 양방향 큐
- i번째 데이터에 접근 : `O(N)`
- 맨 앞/뒤 데이터에 접근/추가/삭제 :` O(1)`
- 탐색 : `O(N)`

<br>

[⬆️ 처음으로](#-contents)

### 5. HashMap 에 대해 설명헤 주세요.
- 비선형 자료구조
- 일정 크기의 배열(버킷)을 생성한 후에 Key 값을 Hash 함수를 통해 배열의 index 로 변환하여, 해당 index 에 해당 Key 값 과 Value 값을 저장
- i 번째 데이터에 접근 : `none` / `O(N)`
- X 라는 Key 가 있는지 탐색 `containsKey()` : `O(1)`
- X 라는 value 가 있는지 탐색 `containsValue()` : `O(n)`
- 키가 X 인 데이터에 접근 :` O(1)`
- X 라는 Key 의 삽입, 삭제 : `O(1)`

<details>
<summary>꼬리질문</summary>
<div markdown="1">

### 해쉬 충돌시 어떻게 해결하는지 설명해 주세요.

#### Open Addressing
- 해쉬 충돌이 발생한 후 비어있는 버킷을 찾아서 저장
- 해쉬 충돌이 발생한 경우 탐색 / 접근의 시간복잡도는 O(N) 으로 증가
- 비어있는 버킷을 찾는 알고리즘
  - Linear Probing (선형 프로빙)
  - Quadratic Probing (이차식 프로빙)
  - Double Hashing (이중 해시)
     

#### Chaining
- 해시 충돌이 발생한 버킷에 `LinkedList` 를 만들고, 해당 `LinkedList` 에 데이터를 저장
- 같은 해쉬에 충돌한 key 가 7개 이하일 경우 `LinkedList` 를 사용하고 8개부터는 `Red-black Tree` 를 사용


</div>
</details>

<br>

[⬆️ 처음으로](#-contents)

### 6. Heap 에 대해 설명헤 주세요.

<br>

[⬆️ 처음으로](#-contents)

### 7. BST 에 대해 설명헤 주세요.

<br>

[⬆️ 처음으로](#-contents)

<br>
<br>