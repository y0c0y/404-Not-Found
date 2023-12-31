- 둘 이상의 프로세스들이 자원을 점유한 상태에서 서로 다른 프로세스가 점유하고 있는 자원을 요구하며 무한정 기다리는 현상을 의미
- 발생 조건
	- 멀티 프로그래밍 환경에서 한정된 자원을 얻기 위해 서로 경쟁하는 상황에서 발생
	- 4가지 조건이 충족되어야 발생
		- [[상호배제 (Multal Exclusion)]]
		- [[점유와 대기 (Hold and Wait)]]
		- [[비선점 (Non-preemption)]]
		- [[환경 대기 (Cirular Wait)]]
	- 해결 방안
		- [[예방 (Prevention)]]
		- 회피 (Avoidance)
			- 교착상태가 발생할 가능성을 배제하지 않고 교착상태가 발생하면 적절히 피해나가는 방법으로, 주로 [[은행원 알고리즘 (Banker's Algorithm) | 은행원 알고리즘]]이 사용된다.
		- 탐지 (Detection)
			- 시스템에 교착상태가 발생했는지 교착상태에 있는 프로세스와 자원을 발견한다.
				- 교착상태 발견 알고리즘과 자원 할당 그래프 등을 사용할 수 있음.
		- 복구 (Recovery)
			- 교착 상태를 일으킨 프로세스를 종료하거나 교착상태의 프로세스에 할당된 자원을 선점하여 프로세스나 자원을 회복한다.



