-  [[커널]]로부터 프로세스에게 할당된 일반적인 메모리 페이지
- 힙을 거치지 않고 할당받은 메모리 공간(e.g [[힙(heap)]])
    - 익명이란? 파일에 기반하고 있지 않은( 파일로부터 매핑되지 않은) 페이지
    - 파일에 매핑되어 있지 않았기 때문에 0으로 초기화된 값을 담고 있다.  
        
- 프로세스가 mmap()으로 커널에게 익명 페이지를 할당 요청하게 되면, 커널은 프로세스에게 가상 메모리 주소 공간을 부여하게 됨.
    - 부여된 가상 메모리 공간은 아직까지 실제 물리 메모리 페이지로 할당되지 않은 공간
    - 메모리 읽기 쓰기시. 커널의 도움을 받아 zero페이지로 [[에뮬레이션 (Emulation)]]

``` C
@/include/vm/anon.h

struct anon_page {
    struct page anon_p;
};
```


