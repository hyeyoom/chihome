# Mini-LSM

[Rust](https://rust-lang.org/)로 작성된 [mini-lsm](https://skyzh.github.io/mini-lsm/00-preface.html) 코스를 학습하는 글이다. 하지만 나는 코틀린으로 한다. 대신 라이브러리 안쓰고 순수하게.  
어쨌든 이런걸 만들게 된다.

![mini-lsm-overview](/images/20260222SUN/mini-lsm-overview.png)  

후회되죠? 찍먹하다가 말겠죠?  

## LSM 개요

LSM 스토리지는 일반적으로 다음과 같은 세 부분을 포함한다고 한다.  

- 장애 복구를 위해 임시 데이터를 디스크에 기록하는 Write-Ahead Log (WAL)
- 디스크 위에서 LSM 트리 구조를 유지하는 SST
- 작은 쓰기를 모아서 처리하기 위한 메모리 내 구조인 memtable

제공하는 인터페이스는 다음과 같다.  

- `Put(key, value)`: LSM 트리에 키-값 쌍을 저장
- `Delete(key)`: 키와 그에 대응하는 값을 삭제
- `Get(key)`: 키에 대응하는 값을 조회
- `Scan(range)`: 범위 내의 키-값 쌍을 조회

영속성 인터페이스

- `Sync()`: Sync 이전의 모든 연산이 디스크에 기록되었음을 보장

## Write Path

![mini-lsm-overview](/images/20260222SUN/write-path.png)  

LSM의 쓰기 경로는 네 단계로 구성:
1. 스토리지 엔진이 장애 발생 후 복구할 수 있도록  키-값 쌍을 WAL에 기록.
2. 키-값 쌍을 memtable에 기록. (1)과 (2)가 완료되면 사용자에게 쓰기 완료를 알릴 수 있다.
3. (백그라운드 작업) memtable이 가득 차면 이를 immutable memtable로 전환(freeze) 하고 디스크에 SST 파일로 flush.
4. (백그라운드 작업) LSM 트리의 형태를 적절히 유지하고 read amplification을 낮추기 위해 일부 레벨의 파일들을 더 낮은 레벨로 compaction.

여기서 read amplification은 논리적 읽기(`Get(key)`)를 수행하기 위해 실제로 몇 번의 디스크/메모리 접근을 해야하는 것을 의미한다. 당연히 덜 해야 좋다.

## Read Path

![mini-lsm-overview](/images/20260222SUN/read-path.png)  

키를 읽을 때는:
- 먼저 가장 최신 것부터 가장 오래된 순서로 모든 memtable을 조회(probe)
- 거기에서 키를 찾지 못하면, SST들로 이루어진 전체 LSM 트리를 탐색하여 데이터를 찾음

읽기에는 두 가지 종류가 있음:
- Lookup: LSM 트리에서 하나의 키를 찾는 것
- Scan: 스토리지 엔진에서 특정 범위에 포함된 모든 키-값 쌍을 순회하는 것

