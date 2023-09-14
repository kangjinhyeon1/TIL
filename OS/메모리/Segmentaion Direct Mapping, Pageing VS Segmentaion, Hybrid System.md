## Segmentaion Direct Mapping

1. 프로세스의 SMT가 저장되어 있는 주소b에 접근
2. 해당 SMT에서 Segment에 대한 entry 찾음
3. 찾아진 entry의 존재 비트검사
    1. Residence bit = 0 - missing
    swapdevice에서 해당 segment를 메모리로 적재후 주소 확인
    2. d가 segment보다 큰 경우(d > k)
    segment overflow exception 처리 모듈 호출
    3. 허가되지 않은 연산일 경우(protection bit field검사)
    segment protection exception 처리모듈 호출
4. 찾은 주소와 가상 주소의 변위d를 사용하여 실제 주소 r확인
5. r로접근

## Paging VS Segmentation

### Paging

- 고정된 크기의 block(page)로 분할
- 관리면에서 낮은 overhead
- 내부단편화 현상 발행
- 공유와 보호가 복잡
- 필요한 페이지만 페이지 프레임에 적재하여 사용 → 메모리 효율적 활용

### Segmentation

- 가변적인 논리 단위 segment로분할
- 관리면에서 높은 overhead
- 외부단편화 현상 발생
- 공유와 보호의 지원이 편리함
- 필요한 세그먼트만 메모리에 적재하여 사용 → 메모리의 효율적 활용

## Hybrid System

- 프로그램을 segment로 나눔
- segment를 page로나눔
- page 단위로 적재
- v = (s, p, d) → (segment, page, displacement)
- SMT, PMT 모두 사용
- Table이 늘어나는 만큼 메모리 소모가 큼
- mapping 과정이 복잡함 → 접근 시간도 늘어남
- 외부 단편화 x, 내부 단편화 O