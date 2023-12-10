- CPU가 유휴 상태가 될 때마다, Ready Queue에 있는 프로세스 중에서 하나를 선택해 실행.
- 선택 절차는 CPU 스케쥴러에 의해 수행
- CPU 스케쥴러는 실행 준비가 되어 있는 메모리 내의 [[프로세스 (Process) | 프로세스]] 중에서 선택하여, 이들 중 하나에게 CPU를 할당함.

- 선점 및 비선점 스케쥴링 (Preemptive and Nonpreemptive Scheduling)
	- CPU 스케쥴링의 결정은 다음 네 가지 상황에서 발생할 수 있음
	1.  한 프로세스가 실행 상태에서 대기 상태로 전환될 때 (I/O 발생)
	2. 프로세스가 실행 상태에서 준비 완료 상태로 전환될 때 (인터럽트 발생)
	3. 프로세스가 대기 상태에서 준비 완료 상태로 전환될 때 (I/O 종료)
	4. 프로세스가 종료할 때
- 비선점 스케쥴링(nonpreemptive)
	- 일단 CPU가 한 프로세스에 할당되면 프로세스가 종료하든지, 또는 대기 상태로 전환해 CPU를 방출할 때까지 점유(1, 4)
- 선점 스케쥴링(preemptive)
	- 시분할 시스템에서 타임 슬라이스가 소진되었거나, 인터럽트나 시스템 호출 종류시에 더 높은 우선 순위 프로세스가 발생 되었음을 알았을 때, 현 실행 프로세스로부터 강제로 CPU를 회수하는 것(2, 3)
- 데이터가 다수의 프로세스에 의해 공유될 때 [[Race Condition | racing condition]]이 발생 될 수 있음
- [[뮤텍스 (Mutex) | mutex lock]], [[모니터 (Monitor) | monitior]]

- [[FCFS (First Come First Served)]]
- [[SJF (Shortest Job First)]]
- [[SRTF (Shortest Remaining Time First)]]
- [[Round Robin]]
- [[Multilevel Queue Scheduling]]
