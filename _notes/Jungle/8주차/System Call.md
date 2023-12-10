[[시스템 콜]]

- OS는 다양한 서비스들을 수행하기 위해 하드웨어를 직접적으로 관리함.
- 응용 프로그램은 OS가 제공하는 인터페이스를 통해서만 자원을 사용할 수 있음.

- OS가 제공하는 인터페이스를 '시스템 콜(System Call)'이라고 함.
	- 커널 영역의 기능을 사용자 모드가 사용 가능하게, 즉 프로세스가 하드웨어에 직접 접근해서 필요한 기능을 할 수 있게 해줌.
		- 응용프로그램은 시스템 콜을 사용해서 원하는 기능을 수행할 수 있음.
		- 직접적으로 시스템 콜을 사용하기 보다는 API(라이브러리 함수)를 통해 사용하게 된다.
		- ![[시스템 콜 구조.png]]
		> OS는 메모리에 프로그램 적재, I/O처리, 파일시스템 처리 등 여러 서비스들을 제공하는데, 사용자 프로세스는 이에 직접적인 접근이 아닌 시스템 콜 호출을 통해 서비스를 제공받을 수 있다.
		
- 시스템 콜 종류
	1. **프로세스 제어 (Process Control)**
	    - 끝내기(exit), 중지 (abort)
	    - 적재(load), 실행(execute)
	    - 프로세스 생성(create process) - fork
	    - 프로세스 속성 획득과 속성 설정
	    - 시간 대기 (wait time)
	    - 사건 대기 (wait event)
	    - 사건을 알림 (signal event)
	    - 메모리 할당 및 해제
	2. **파일 조작 (File Manipulation)**
	    - 파일 생성 / 삭제 (create, delete)
	    - 열기 / 닫기 / 읽기 / 쓰기 (open, close, read, wirte)
	    - 위치 변경 (reposition)
	    - 파일 속성 획득 및 설정 (get file attribute, set file attribute)
	3. **장치 관리 (Device Manipulation)**
	    - 하드웨어의 제어와 상태 정보를 얻음 (ioctl)
	    - 장치를 요구(request device), 장치를 방출 (relese device)
	    - 읽기 (read), 쓰기(write), 위치 변경
	    - 장치 속성 획득 및 설정
	    - 장치의 논리적 부착 및 분리
	4. **정보 유지 (Information Maintenance)**
	    - getpid(), alarm(), sleep()
	    - 시간과 날짜의 설정과 획득 (time)
	    - 시스템 데이터의 설정과 획득 (date)
	    - 프로세스 파일, 장치 속성의 획득 및 설정
	5. **통신 (Communication)**
	    - pipe(), shm_open(), mmap()
	    - 통신 연결의 생성, 제거
	    - 메시지의 송신, 수신
	    - 상태 정보 전달
	    - 원격 장치의 부착 및 분리
	6. **보호 (Protection)**
	    - chmod()
	    - umask()
	    - chown()
![[시스템 콜 종류.png]]

- C 언어에서의 시스템 콜
	-  POSIX(Portable Operating System Interface)의 규정에 따라 함수를 제공하고 있으며, OS개발사 또는 컴파일러 개발사에서 추가적인 확장 API들을 제공하는 것이 일반적
	- C언어를 활용하여 개발하는 개발자 입장에서는 시스템콜 함수이든, 라이브러리 콜 함수이든 단지 함수의 형태이므로 특별히 구별되지는 않을 것
	- 그러나 system call function이 자주 호출되면 시스템 성능에 영향을 주기 때문에 최대한 알고 쓰고, 자제 해야 한다.