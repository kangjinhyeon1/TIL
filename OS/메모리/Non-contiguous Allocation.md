## 개념

- 프로그램을 블록으로 나눔
- 필요한 블록만 가져와서 사용
- 나머지는 swap device에 존재
- paging
- segmentaion
- hybrid

## Memory mapping

### virtual address = logical = 논리적 주소

- 연속된 메모리 할당을 가정한 주소

### real address = physical = 물리적 주솧

- 실제 메모리에 적재된 주소

## Block Mapping

- 프로그램을 Block 단위로 분활핟여 관리
- 메모리도 Block size로 미리 분할 하여 관리
- External Fragmentation 없음
- 프로그램의 논리적 구조 고려 x
- v = (b, d) = real address
b: block number
d: diplacemet in a block(offset)

## Block map table(BMT)

### BMT

테이블이 가지고 있는 3가지

- block number
- residence bit: 해당 블록이 메모리에 적재 되었는지 여부를 0과 1로 표시
- real address

## 실행 과정

<img src="https://github.com/corrni/sketch-viewer/assets/100929676/030ec9fc-7e40-4a11-a235-fc68e9439370">

1. 프로세스 BMT 접근
2. BMT에서 block b 에 대한 칸 찾음
3. residence bit 검사
    1. 0인 경우 - swap device에서 블록을 메모리로 가져와서 BMT 업데이트 후 , real address 값 확인
    2. 1인 경우 - b에해닿ㄴ real address 값 확인
4. 실제 주소 r 계산(r = a + d)
5. r을 이용하여 메모리에 접근

1~2는 b를 구하는 것

3은 a를 찾는 과정

4~5는 real 주소를 찾는 것이다.