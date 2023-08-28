## Contiguous Allocation(연속할당) - Memory Mapping

### Relative address(상대주소)

- 프로그램의 시작 주소를 0으로 가정한 주소

### Relocation(재배치)

- 메모리에 할당한 후 할당된 주소에 따라 주소들을 조정하는 작업

## Dynamic Loading

- 모든 루틴을 교체 가능한 형태로 디스크에 저장
- 함수 호출시에 → 바인딩 → 호출전에는 적재 x
- 효율이 높아짐

<img width="832" alt="다이나믹 로딩" src="https://github.com/AI-Expo-2023/Chromatica-Client-V1/assets/100929676/ff95ecab-8fce-49e7-b496-ab8e199cd849">

## Overlay

- 실행하려는 프로그램이 메모리 보다 클때, 필요 없는 영역에 중첩하여 사용

## Swapping

- 중기 스케줄러에서 스케줄링을 위해 메모리에 올라온 프로세스의 수를 조절하는 방법
- Ram → swap-out(할당끝, 수행완료) → swap device
- swap device → swap-in(새로운 시작) → RAM
1. 대신 어떤 자원도 사용 중 이면 안됨
2. 특히, 입출력 장치
3. 중기 스케줄러가 관여함