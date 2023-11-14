- 명시적 가용 리스트(Explicit Free List)
    - explicit
        - 할당이 해제되어있는 블록들을 연결리스트 형태로 관리하여 모든 블록을 검사하지않고, 할당이 해제된 블록들만 검사하는 방법.
        - implicit에 next-fit 방식의 성능과 유사함.
    - 연결리스트에 블록을 추가하는 방식에 따라 블록의 물리적인 순서대로 연결리스트가 구성되는 **ordered-list방식(단편화 방지 측면 GOOD)**과 최신에 해제된 블록을 연결리스틔의 가장 앞에 추가하는 **LIFO방식(성능 측 GOOD)**으로 나뉨.
    - 설명은 LIFO방식
        - !**물리적 순서와 연결리스트의 순서가 같음을 보장하지 않음**.
    - implicit 방식과 달리 header와 footer이와에 **prev & next block pointer**가 들어감.
    - 이 정보들을 이용해 해제된 블록들을 **연결리스트의 형태로 관리**.
    - 가장 앞 블록은 할당이 돼있는 블록으로 연결리스트에 들어가 있어 **연결리스트의 끝점을 나타내는 역할**을 수행

[![](https://blog.kakaocdn.net/dn/byEpfI/btsAkmGvYTI/bNrsgrOMy6aTGIicegK5Kk/img.jpg)](https://velog.io/@emplam27/CS-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%8F%99%EC%A0%81%ED%95%A0%EB%8B%B9-Implicit-Explicit-Segregated-list-Allocator#implicit-allocator)

출처 : emplam27

---

- 메모리 할당과정
    - 할당 되어있는 블록의 경우에는 연결리스트에서 관리하지 않기 때문에 prev, next 정보는 필요하지 않음.

1. 연결리스트의 처음부터 순회하면서 블록의 **사이즈를 확인**합니다. 연결리스트 내의 블록들은 마지막 블록을 제외하고는 이미 모두 할당이 해제된 블록입니다.
2. 블록의 사이즈가 본인보다 작다면 할당할 수 없는 공간입니다. 해당 블록의 **next 포인터로 이동**하여 다음 블록을 검사합니다.
3. 블록의 사이즈가 본인보다 크거나 같다면 할당할 수 있는 공간입니다.  
    3-1. 해당 블록을 **연결리스트에서 제거**합니다.  
    3-2. 메모리가 할당될 수 있는 사이즈 공간을 초과한다면 **블록을 분할**하여 할당하고, **나머지 부분을 해제된 블록**으로 바꿔준 후 **연결리스트에 추가**합니다.  
    3-2. **메모리를 할당**하고 해당 블록의 block pointer **주소를 반환**합니다.
4. 할당할 수 있는 공간이 없어 연결리스트의 끝에 도달했다면 힙을 확장하여 할당합니다.
5. 추가적으로 3-2 과정에서 분할된 블록의 사이즈가 일정 수준보다 작은 사이즈가 만들어지게 되는 경우라면, 해당 블록을 전부 사용하여 외부 단편화를 방지합니다.

[![](https://blog.kakaocdn.net/dn/oxsjS/btsAkk2YPe6/wrdG29Ykr145wmjaT9kqj0/img.jpg)](https://velog.io/@emplam27/CS-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%8F%99%EC%A0%81%ED%95%A0%EB%8B%B9-Implicit-Explicit-Segregated-list-Allocator#implicit-allocator)

출처 : emplam27

---

- 메모리 할당 해제 과정

1. 할당을 해제할 메모리 주소를 받습니다. 해제할 메모리 주소의 **앞뒤에 블록들을 확인**합니다.
2. 할당을 해제할 블록의 앞 또는 뒤에 이미 할당이 해제된 블록이 존재한다면 해당 블록들을 **연결리스트에서 제거**합니다.
3. 이후 제거한 블록들과 합쳐 **하나의 할당 해제상태 블록**으로 만들고, **연결리스트의 가장 앞에 추가**합니다.

[![](https://blog.kakaocdn.net/dn/cmkiZc/btsAkiD5GNV/OqyMTA5nGrLUq0Q5ebR73k/img.jpg)](https://velog.io/@emplam27/CS-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%8F%99%EC%A0%81%ED%95%A0%EB%8B%B9-Implicit-Explicit-Segregated-list-Allocator#implicit-allocator)

출처 : emplam27