## 해시 함수(Hash Function)

<img src = "https://velog.velcdn.com/images/jonghyeok98/post/9218cb6e-09a5-442d-92c9-03f77e5c383e/image.png" width = 600>

- 해시(Hash)는 입력 데이터가 고정된 길이의 데이터로 변환된 값으로 해시 함수에 의해 얻게 됩니다.



## 해시 테이블(Hash Table)

<img src = "https://velog.velcdn.com/images/jonghyeok98/post/796b0f61-4b32-4d78-ab06-b9d00a3e7eff/image.png">

- Hash Table은 Key와 Value를 쌍으로 갖는 자료구조로 Hash Map이라고도 불립니다.
- 배열의 인덱스에 해시 값을 사용하는 자료구조로 Associative Array ADT(=Map ADT)를 구현하는데 사용됩니다.
- 데이터를 저장하기 위해 충분히 큰 공간을 할당받은 다음 해시 함수를 이용하여 고유 인덱스를 생성한 후 해당 인덱스에 맞는 위치에 데이터를 저장합니다.
- 정렬을 하지 않고도 삽입, 탐색이 $O(1)$의 시간 복잡도를 가집니다.

> - 버킷(Bucket):
> - 슬롯(Slot): 


***만약 "State"와 "County"의 Hash가 같다면 무슨 일이 발생할까?***


## 해시 충돌(Hash Collision)
- key가 다르더라도 동일한 해시 값을 갖게 되는 것을 해시 충돌(Hash Collision)이라고 합니다.
- 해시 충돌은 불가피하기 때문에 충돌이 발생할 확률을 떨어트림으로써 최대한 충돌을 피해야합니다.





## 체이닝(Chaining)
- 해시 충돌이 발생해 동일한 인덱스가 나오면 해당 인덱스에 추가로 이어서 저장하는 방법

<img src = "https://velog.velcdn.com/images/jonghyeok98/post/15ce3c8a-e119-4785-8985-963058ef9e89/image.png" width = 800>

- 해시 테이블의 각 버킷(Bucket)에 연결 리스트 또는 다른 자료 구조를 이용하여 어러 개의 키를 저장하는 방식입니다.

### 체이닝의 장점
- 해시 테이블 크기보다 많은 키를 저장할 수 있으며 해시 충돌 시 버킷 내 리스트를 확장하면 되므로 고정 크기의 제약을 받지 않습니다.
- 충돌이 발생해도 리스트를 통해 키를 관리하므로 다른 버킷에 영향을 주지 않습니다.
- 연결 리스트에서 노드만 제거하면 되므로 간단하게 삭제가 가능합니다.

### 체이닝의 단점
- 해시 함수가 좋지 않거나 키가 너무 많을 경우 리스트의 길이가 길어져 성능이 저하됩니다.
- 리스트의 길이가 길수록 탐색, 삽입, 삭제의 평균 시간이 $O(N)$에 가까워질 수 있습니다.
- 각 버킷의 리스트를 위한 추가적인 메모리가 필요합니다.

## 오픈 어드레싱(Open Addressing)
- 해시 충돌이 발생하면 해당 인덱스가 아닌 다른 인덱스에 저장하는 방법으로 개방 주소법이라고도 합니다.

<img src = "https://velog.velcdn.com/images/jonghyeok98/post/59f58b50-7b19-4789-9999-dde94e7d9ca7/image.png" width = 700>

### 선형 탐사(Linear Probing)
- 충돌이 발생하면 해당 위치를 기준으로 고정된 간격으로(일반적으로 1) 다음 위치를 순차적으로 탐색합니다.
- 충돌된 키들이 연속된 영역을 차지하며 클러스터링 문제가 발생할 수 있으며 새로운 충돌 발생 시 탐색 시간이 증가합니다.


### 제곱 탐사(Quadratic Probing)
- 충동리 발생했을 때 탐색 간격이 $i^2$로 증가합니다.
- 선형 탐사의 클러스터링 문제를 완화할 수 있습니다.
- 해시 테이블의 크기가 적절하지 않으면 재탐사 불가 문제가 발생할 수 있습니다.
	- 테이블의 크기는 일반적으로 소수로 설정합니다.


### 이중 해싱(Double Hashing)
- 충돌 시 새로운 해시 함수를 통해 탐사 간격을 결정합니다.
- 클러스터링 문제를 크게 줄이며 키의 분포가 훨씬 균일해집니다.
- 해시 함수 두 개를 구현해야 하므로 추가 비용이 발생합니다.

|방법|충돌 해결 방식|장점|단점|
|---|---|---|---|
|선형 탐사|고정 간격으로 순차 탐색| - 간단한 구현<br> - 효율적 메모리 사용|클러스터링 발생|
|제곱 탐사|증가 폭이 $i^2$인 간격 탐색|클러스터링 감소|테이블 크기 제약
|이중 해싱|두 번째 해시 함수 사용| - 충돌 최소화<br> - 균일 분포|추가 해시 함수 비용|


### 체이닝 vs 오픈 어드레싱

|특징|체이닝|오픈 어드레싱|
|---|---|---|
|충돌 해결 방식|버킷에 연결 리스트 사용|테이블 내 빈 공간을 찾아 재탐색|
|메모리 사용량|더 많은 메모리 필요|테이블 크기 내에서 관리|
|성능|좋은 해시 함수일 경우 평균적으로 빠름|충돌 많으면 성능 저하 가능|
|삭제|리스트에서 간단히 삭제 가능|삭제된 공간 관리가 복잡할 수 있음|


<img src = "https://velog.velcdn.com/images/jonghyeok98/post/f48bd4db-a2e1-4611-b986-523d76380281/image.png" width = 700>



### 언어별 해시테이블의 방식

|언어|방식|
|---|---|
|C++|체이닝|
|C#|오픈 어드레싱|
|Java|체이닝|
|Python|오픈 어드레싱|


## 질문
### 1. Hast Table이란 ?
### 2. 해시 충돌이 발생하는 경우와 어떻게 해결하는지
### 3. 해시 테이블 삽입 시 $O(N)$이 걸리는 경우
