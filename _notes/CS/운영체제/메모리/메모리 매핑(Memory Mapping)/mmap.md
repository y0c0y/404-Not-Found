
```C
    #include <sys/mman.h>
     void *mmap(void *addr, size_t len, int prot, int flags, int fildes, off_t off);
``` 

- 지정된 파일을 메모리에 매핑시키는 기능을 수행
- 메모리에 매핑된 내용에 접근할 수 있는 **포인터**를 반환, 에러시 return **-1**
- prot인자는 원하는 메모리 보호모드를 설정
   - **PROT_EXEC :** 페이지는 실행 가능하다.
   - **PROT_READ :** 페이지는 읽을 수 있다.
   - **PROT_WRITE :** 페이지는 쓰여질 수 있다.
   - **PROT_NONE :** 페이지는 접근할 수 없다