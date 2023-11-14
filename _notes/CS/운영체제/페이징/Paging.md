- 논리주소의 메모리를 고정된 크기의 페이지로 나누어 관리하는 기법.
    - **페이지 테이블을 이용해 논리주소에서 프레임을 가리키는 물리주소로 매핑.**
        - pre-process 데이터 구조. 즉, 모든 프로세스가 페이지 테이블을 가지고 있음.
        - 페이지 테이블은 메인 메모리에 저장됨. 
        - PTBR(Page Table Base Register) - 페이지 테이블을 가리키고 있음.
        - PTLR(Page Table Length Register) - 페이지 테이블의 사이즈를 가리키고 있음.
        - 이러한 레지스터들의 내용은 PCB에 저장되어 있음. -> **[[문맥 교환(context switching)]]**이 일어날 때 교체됨.
            - Process의 Context란 프로그램 카운터(PC), CPU 레지스터들의 값, 메모리 관리 상태 등을 포함한 프로세스의 상태를 뜻하는데, Context Switching은 종작 중인 프로세스의 상태를 PCB에 보관하고 context를 바꿀 프로세싱 상태를 불러와 복구하는 과정.
        - 모든 data/instruction 접근은 두 번의 메모리 접근이 필요하다 -> **페이지 테이블에 접근하는 overhead가 존재한다.**
            - fast-lookup hardware cache라고 불리는 associative maemory 혹은 translation look-aside buffers([[TLB]]s)를 이용해 해결할 수 있다.
                - 가상 메모리 주소를 물리적인 주소로 변환하는 속도를 좁이기 위해 사용되는 캐시
                - 최근에 일어난 가상 메모리 주소와 물리 주소의 변환 테이블을 저장하기 때문에 일조의 주소 변환 캐시라고 할 수 있음
    -  **외부 단화는 발생하지 않으나, 내부 단편화는 발생.**
        - 페이지 단위를 작게하면 내부 단편화 문제도 해결할 수 있겠지마, 대신 page mapping 과정이 많아지므로 오히려 효율이 떨어질 수 있음.                                                                                                                                                                             

[![](https://blog.kakaocdn.net/dn/Q9xer/btsAal33Q5J/ATRr568Lhs9jn9DbYWsYkk/img.png)](https://code-lab1.tistory.com/55)
출처 : _연구소장_