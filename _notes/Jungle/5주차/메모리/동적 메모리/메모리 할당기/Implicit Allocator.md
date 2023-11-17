  

![](https://blog.kakaocdn.net/dn/bdgT58/btsAjjKf0vS/Fk5jcRXqTuHO0u13xBqg60/img.png)

출처 : CS:APP

- 묵시적 가용 리스트(Implicit Free List) 
    - implicit 
        - 순차적으로 모든 블록을 검사하는 선현적인 방법. 일종의 부르트포스 방식
        - first-fit방식을 사용하면 성능이 떨어짐. next-fit 방싱을 사용하면 성능을 매우 향상시킬 수 있음.
    - But, 설명은 first-fit 방식
    - heap의 가장 처음과 끝 4byte는 힙의 처음과 끝을 알 수 있게 하는 블록. 사이즈는 0, 할당여부는 1인 정보를 부여함. 이후 , 가장 처음 블록은 header와 footer이외에 어떠한 정보도 들어있지 않은 initial block을 설정함. **모든 탐색은 해당 블록으로 부터 시작**할 수 있게하기 위함.
    - 모든 방식에서 블록의 포인터(block pointer)를 활용하여 탐색을 수행하게 됨.
        - 이는 header칸의 바로 뒤 주소로 하는데, block pointer와 할당된 메모리의 주소가 같아 바로 반환하여 사용자에게 메모리가 저장된 위치를 바로 알려줄 수 잇어 해당 위치로 잡은것

[![](https://blog.kakaocdn.net/dn/6Wh2f/btsAiE2gEhL/oicZj201kkTvzP13jep4u0/img.jpg)](https://velog.io/@emplam27/CS-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%8F%99%EC%A0%81%ED%95%A0%EB%8B%B9-Implicit-Explicit-Segregated-list-Allocator#implicit-allocator)

출처 : emplam27

---

- 메모리 할당 과정

1. 탐색을 진행하는 블록의 header 또는 footer를 확인하여 해당 블록의 **할당 여부를 확인**합니다.
2. 할당이 되어있다면, 블록의 사이즈만큼 옆으로 이동하여 **다음 블록을 확인**합니다.
3. 할당이 되어있지 않다면, 블록의 사이즈를 확인합니다.  
    3-1. 메모리가 할당될 수 있는 사이즈 공간과 같다면 **메모리를 할당**하고 해당 블록의 block pointer **주소를 반환**합니다.  
    3-2. 메모리가 할당될 수 있는 사이즈 공간을 초과한다면 **블록을 분할**하여 할당하고, **나머지 부분을 해제된 블록**으로 바꿔줍니다.  
    3-3. 메모리가 할당될 수 있는 사이즈보다 작은 공간이라면 블록의 사이즈만큼 옆으로 이동하여 **다음 블록을 확인**합니다.
4. 할당할 수 있는 공간이 없어 힙의 끝에 도달했다면 힙을 확장하여 할당합니다.
5. 추가적으로 3-2 과정에서 분할된 블록의 사이즈가 일정 수준보다 작은 사이즈가 만들어지게 되는 경우라면, 해당 블록을 전부 사용하여 외부 단편화를 방지합니다.

![](https://blog.kakaocdn.net/dn/YTeSl/btsAeA0jsaX/NnLKGSh9m0KeH5p94NJKkk/img.jpg)

- 메모리 할당 해제과정

1. 할당을 해제할 메모리 주소를 받습니다. 해제할 메모리 주소의 **앞뒤에 블록들을 확인**합니다.
2. 할당을 해제할 블록의 앞 또는 뒤에 이미 할당이 해제된 블록이 존재한다면 해당 블록과 합쳐 **하나의 할당 해제상태 블록**으로 만들어 외부 단편화를 방지합니다.

[![](https://blog.kakaocdn.net/dn/EuPhJ/btsAjSey5i9/3PtIwDkBTSdNUhQ4U7Sel1/img.jpg)](https://velog.io/@emplam27/CS-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%8F%99%EC%A0%81%ED%95%A0%EB%8B%B9-Implicit-Explicit-Segregated-list-Allocator#implicit-allocator)

출처 : emplam27