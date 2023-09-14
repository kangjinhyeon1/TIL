## Page Sharing

- 여러 프로세스가 특정 Page공유
- 공유가능한 page
    - procedure pages
        - pure code creentrantcode: 수행되는 동한 절대 편하지 않는 코드
    - pata page
        - read - only data
        - read write data 병행성 제어 기법과 같이 사용

## Page Protection

여러 프로세스가 page를 공유할 때, protection bit 사용

- valid 타당비트: 메인메모리 적재되었는지
- read 읽기 비트: 읽ㄱ 여부
- write쓰기 비트: 쓰기 여부
- Excution: 실행 비트, 실행 여부

## Segmentation

- segment: 서로 다른 크기를 갖는 논리적인 단위
- 서브 루틴이나 함수 들의 단위를 나누거나 행렬이나 스택 등의 대 단위 자료 구조 등에 이름을 부여하는 적재
- 메모리를 미리분할 하지않음
- 세그먼트 공유와 보호가 용이함
- 주소 mapping, 메모리 관리 → hign overhad

### Mapping

- v=(s,d)
- segment map table(SMT)