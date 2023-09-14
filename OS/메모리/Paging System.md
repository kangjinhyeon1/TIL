# Paging System

## 개념

- 페이지(P): 프로세스의 block
- 페이지 프레임(p’): 메모리의 분할 영역, 페이지와 크기 같음
- V = (p,d)
- 프로그램이 756일 때, 페이지의 크기는 150이다. 그럼 페이지는 몇개고, 크기는 각각 어떻게 되는가?
- 150이 5개, 마지막 하나는 6
- There is no external fragmentation in pagin but internal fragmentation exists
- simple and efficient

## Direct mapping

1. 프로세스의 PMT가 저장되어 있는 주소b에 접근
2. 해당 PMT에서 page p에 대한 entry찾음
3. 찾아진 entry의 존재 비트 검사
    1. Residence bit = 0 - page fault swap device에서 할당 page를 메모리로 적재후 p’확인
    2. Residence bit = 1 - page frame 번호 p’ 확인
4. p’와 가상 주소의 변위 d를 사용 하여 실제 주소 r확인
5. r로 접근

1 ~ 2: b + p * Entry size

4: p’ * page size + d

### 문제점

- 메모리 접근 횟수가 2배 → 성능 저하
- PMT를 위한 메모리 공간 필요

### 해결 방안

- TLB를 이용한 연관 사살(Associative Mapping)
- PMT를 위한 전용 기억장치 사용 → 캐시 메모리