## Associative mapping

- TLB: translation look - aside buffer
- TLB에 BMT를 탑재
- page number를 병렬로 탐색하여 p’를 빠르게 찾음
- low overhead high speed
- expensive hardware

- TLB에 PMT의 일부를 탑재 = AMT
- p’를 찾을 때, AMT부터 접근 → 적중률
    - AMT에 있으먄 residence bit로 p’확인
    - AMT에 없으면 PMT확인 후 AMT에 PMT entry 적재
    - PMT에서 사용되는 entry 지역성을 따져 AMT에 적재

## 학습지 첫번째 문제 풀이

1. CPU → AMT
2. CPU → PMT
3. CPU → p’

(1 → 3) * 적중율 + (1 → 2 → 3) * 적중 실패율