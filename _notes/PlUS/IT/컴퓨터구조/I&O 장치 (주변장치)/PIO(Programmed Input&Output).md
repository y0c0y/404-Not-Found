-  저수준 파일 처리 : [[Jungle/6주차/File Descriptor|File Descriptor]]
	- 번호에 의해 파일 입출력을 함.
	- 비 직관적인 함수 형태를 사용
	- 버퍼링 없는 파일 입출력(Unbuffered File I/O)
	- 프로그래머가 버터 크기를 일일이 지정해주어야 함.
		- open(), write() 등



- 고수준 파일 처리 : [[File Fointer]]
	- FILE 구조체에 의해 파일 입출력을 함. (표준 C언어를 지원하는 모든 [[OS | 운영체제]] 지원)
	- C 언어 표준인 추상화된 FILE 구조체를 사용
	- 표준 입출력 라이브러리로써, 파일에 [[File Stream | 파일 스트림]]을 연관시키는 <stdio.h>에 선언되어있음.
		```C
		#include <stdio.h>

		FILE * fopen (const char *path, const char *mode);
		```
		- 직관적이고 사용이 편리한 함수 형태를 제공.
		- 버퍼링 있는 파일 입출력(Buffered File I/O)
		- 프로그래머가 버퍼크기를 일일이 지정해 주지 않아도 되며, 줄 단위 처리 등이 용이

- UNIX/Linux 파일 I/O 
	- 열려있는 파일을 통한 입출력
		- 모든 열려있는 파일을 참조할 때 [[Jungle/6주차/File Descriptor|File Descriptor]]를 씀.
	- 파일 I/O를 위한 버퍼 캐시
		- 서로 다른 속도의 디스크 저장장치, 메모리 등에서의 읽기 쓰기를 곧바로 해당 장치에다가 즉시 수행하지 않고, 반드시 [[ Buffer | 버퍼]]를 통해서만 접근함.