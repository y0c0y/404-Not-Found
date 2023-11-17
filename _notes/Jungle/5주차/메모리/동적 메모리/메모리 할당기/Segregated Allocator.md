- 명시적 할당기 (Segregated Free List)
    - seg-list 
        - explict에서 사용한 탐색, 할당 삭제의 로직을 그대로 사용함.
        - ex, im을 사용하는 할당기는 한개의 블록을 할당할 때 free block의 수에 비럐하는 시간이 필요하기에, 이를 획기적으로 줄이는 방법이 segregated free list 방식!
        - 할당이 해제되어있는 블록들을 사이즈 별로 모아 다른 연결리스트에 관리하는 방법.
    - ex방식과 동일하게 연결리스트를 만들지마, 사이즈별로 만들어야 하기 때문에 여러개의 연결리스타가 필요
    - **여러개의 연결리스트 포인터를 힙에 저장**하여 특정한 사이즈의 메모리를 할당하고자 하면 해당 사이즈에 맞는 연결리스트로 이동하여 할당할 블록의 위치를 찾음.
    - 할당하는 메모리의 사이즈를 나누는 단위는 정해지지 않았지만 대부분 2n 단위로 나눔.
    - 할당이 해제된 블록을 **유사한 사이즈의 블록들이 모여있는 리스트**에서 찾기 때문에 빠른 속도로 찾을 수 있어 가장 성능이 좋음.
    - 해당 리스트에서 사이즈에 맞는 블록을 찾지 못하면 다음 크기의 리스트로 넘어가서 할당할 블록을 찾게 됩니다. 이 부분만 제외하면 explicit과의 로직이 동일함.

[![](https://blog.kakaocdn.net/dn/cU4UF5/btsAalQEkXH/KZUgL8QZ8qkxSk9tLknKS1/img.jpg)](https://velog.io/@emplam27/CS-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%8F%99%EC%A0%81%ED%95%A0%EB%8B%B9-Implicit-Explicit-Segregated-list-Allocator#segregated-list-allocator)

출처 : emplam27