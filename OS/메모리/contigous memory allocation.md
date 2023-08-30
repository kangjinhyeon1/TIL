<aside>
❓ 프로세스를 연속된 메모리 할당하는 정책
- 몇개가 동시에 올라갈 수 있나?

</aside>

## 1 Process

- 커널, Boundary register 사용
- 메모리 낭비, 시스템 자원 활용(다운), 효율(업)

Process → Kernel(OS) : Boundary register - Kernel 보호

## Fixed partition

- 고정된 크기로 나눠서 할당 → 요청시 할당해줌, 이때 고정된 크기는 모두 같은 크기x
- 메모리 관리 간편 → Low Overread
- 분할 기준 레지스터 값에 논리적 주소를 더해서 물리적 주소생성
- 각 partition 마다 Boundart register가 있음

## Fragmentation

### 프로그램에 의해 사용 x, 낭비되는 부분적인 기억 공간

### Internal Fragmentaion

- partition 크기 > Process 크기
- 분할된 공간 안에서 공간이 남는 것
- 남은 공간은 사용할 수 없는 공간

### External Fragmentation

- 남은 메모리 크기 < Process 크기
- 공간은 있지만 크기가 맞지 않아서 공간이 남는 것
- 처리 가능한 공간

### Variable Partition

- 요청시 동적으로 분할하여 할당
- Bounday register가 있음

## 메모리 할당

- FPM(고정 분할)
- VPM(가변 분할)
- fragment(단편화)
    - internal fragment(내부 단편화)
    - external fragment(외부 단편화)