- page replacement algorithm
- replacement의 목적 -> **cache miss를 최소화**하기 위함.

> **Average Memory access time(AMAT) 
> - 평균 메모리 접근 시간**
> 
> **AMAT = (Phit * Tm) + (Pmiss * Td)**
> 
	-Tm : 메모리에 접근하는 시간
	- Td : 디스크에 접근하는 시간
	- Phit : cache에 찾고자 하는 data가 있을 확률
	- Pmiss : cache에 찾고자 하는 data가 없을 확률
	일반적으로 Td> Tm보다 훨씬 크기 때문에 Pmiss를 줄이는 게 성능 향상에 매우 도움이 됨.



