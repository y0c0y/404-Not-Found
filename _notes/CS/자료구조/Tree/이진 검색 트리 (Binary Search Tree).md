### **이진 트리**

---

[![](https://blog.kakaocdn.net/dn/cVtoPZ/btsyLsDFvnT/ZRzcGtnRpLVBmzGAGfetbk/img.png)](https://yoongrammer.tistory.com/69)

출처 : yoongrammer

- 노드가 왼쪽자식과 오른쪽 자식만을 갖는 트리

- 두 자식 가운데 하나 또는 둘 다 존재하지 않는 노드가 있어도 **상관X**

---

### **완전 이진 트리**

---

[![](https://blog.kakaocdn.net/dn/TCxc8/btsyOHfe6mI/xMHvGmfIcmVxHokrXWPeQ1/img.png)](https://yoongrammer.tistory.com/69 "출처 : yoongrammer 블로그")
출처 : yoongrammer

- 루트부터 아래쪽 레벨로 노드가 가득 차있고, 같은 레벨 안에서 왼쪽부터 오른쪽으로 노드가 채워져 있는 이진트리

- 마지막 레벨에 한해서 왼쪽부터 오른쪽으로 노드를 채우되 반드시 끝까지 채우지 않아도 됨.

- 높이가 K인 완전 이진 트리가 가질수 있는 노드의 수는 최대 2^(k+1) - 1개이므로, n개의 노드를 저장할 수 있는 완전 이진 트리의 높이는 log n

---

### 이진 검색트리(BST)

---

**조건**

- 왼쪽 서브트리 노드의 키값은 자신의 노드 키값보다 작아야함.

- 오른쪽 서브트리 노드의 키값은 자신의 노드 키값보다 커야함.

**특징**

- 구조가 단순

- 중위 순회의 깊이 우선 검색을 통하여 노드값을 오름차순으로 얻을 수 있음.

- 이진 검색과 비슷한 방식으로 아주 빠르게 검색할 수 잇음.

- 노드를 삽입하기 쉬움.

---

### 구현

기본적인 이진 트리

```Python
class Node:
    def __init__(self, key):
        self.left = None
        self.right = None
        self.val = key


class BinaryTree:
    def __init__(self):
        self.root = None

    def insert(self, key):
        if self.root is None:
            self.root = Node(key)
        else:
            self._insert_recursively(self.root, key)

    def _insert_recursively(self, node, key):
        if node is None:
            return Node(key)
        if key < node.val:
            node.left = self._insert_recursively(node.left, key)
        else:
            node.right = self._insert_recursively(node.right, key)
        return node

    def inorder_traversal(self, node, result=None):
        if result is None:
            result = []
        if node:
            self.inorder_traversal(node.left, result)
            result.append(node.val)
            self.inorder_traversal(node.right, result)
        return result

    def display(self):
        nodes = self.inorder_traversal(self.root)
        for node in nodes:
            print(node)


# 예제 사용:
bt = BinaryTree()
bt.insert(5)
bt.insert(3)
bt.insert(8)
bt.insert(1)
bt.insert(4)
bt.insert(7)
bt.insert(9)
bt.display()
```

복잡한 코드

1. 노드 클래스 Node

```Python
from __future__ import annotations
from typing import Any, Type  # 형힌트 지원

class Node:
    """이진 검색 트리의 노드"""
    def __init__(
        self, key: Any, value: Any, left: Node = None, right: Node = None
    ) -> None:
        """생성자(constructor)"""
        self.key = key  # 키
        self.value = value  # 값
        self.left = left  # 왼쪽 자식 포인터
        self.right = right  # 오른쪽 자식 포인터
```

2. 이진 검색 트리 클래스

```Python
class BinarySearchTree:
    def __init__(self) -> None:
        """초기화"""
        self.root = None  # 루트

    def search(self, key: Any) -> Any:
        """주어진 키에 해당하는 값을 찾아 반환"""
        p = self.root
        while True:
            if p is None:
                return None
            if key == p.key:
                return p.value
            elif key < p.key:
                p = p.left
            else:
                p = p.right

    def add(self, key: Any, value: Any) -> bool:
        """키와 값을 가진 노드를 추가"""

        def add_node(node: Node, key: Any, value: Any) -> bool:
            """노드를 서브트리에 추가"""
            if key == node.key:
                return False
            elif key < node.key:
                if node.left is None:
                    node.left = Node(key, value)
                else:
                    return add_node(node.left, key, value)  # 수정: 재귀 호출 시 node.left를 전달
            else:
                if node.right is None:
                    node.right = Node(key, value)
                else:
                    return add_node(node.right, key, value)  # 수정: 재귀 호출 시 node.right를 전달
            return True

        if self.root is None:
            self.root = Node(key, value)
            return True
        else:
            return add_node(self.root, key, value)

    def remove(self, key: Any) -> bool:
        """주어진 키를 가진 노드를 삭제"""
        p = self.root  # 스캔 중인 노드
        parent = None  # 스탠 중인 노드의 부모 노드
        is_left_child = True  # p는 parent의 왼쪽 자식 노드인지 확인

        while True:
            if p is None:
                return False
            if key == p.key:
                break
            else:
                parent = p
                if key < p.key:
                    is_left_child = True
                    p = p.left
                else:
                    is_left_child = False
                    p = p.right
        if p.left is None:
            if p is self.root:
                self.root = p.right
            elif is_left_child:
                parent.left = p.right
            else:
                parent.right = p.right
        elif p.right is None:
            if p is self.root:
                self.root = p.left
            elif is_left_child:
                parent.left = p.left
            else:
                parent.right = p.left
        else:
            parent = p
            left = p.left
            is_left_child = True
            while left.right is not None:
                parent = left
                left = left.right
                is_left_child = False
            p.key = left.key
            p.value = left.value
            if is_left_child:
                parent.left = left.left
            else:
                parent.right = left.right
            return True

    def dump(self, reverse=False) -> None:
        """트리를 순회하여 모든 노드를 출력"""

        def print_subtree_rev(node: Node):  # 내림차순
            if node is not None:
                print_subtree(node.right)
                print(f"{node.key} {node.value}")
                print_subtree(node.left)

        def print_subtree(node: Node):  # 오름차순
            if node is not None:
                print_subtree(node.left)
                print(f"{node.key} {node.value}")
                print_subtree(node.right)

        print_subtree_rev(self.root) if reverse else print_subtree(self.root)


    def min_key(self) -> Any:
        """트리에서 가장 작은 키를 가진 노드의 키를 반환"""
        if self.root is None:
            return None
        p = self.root
        while p.left is not None:
            p = p.left
        return p.key

    def max_key(self) -> Any:
        """트리에서 가장 큰 키를 가진 노드의 키를 반환"""
        def max_key(self) -> Any:
        if self.root is None:
            return None
        p = self.root
        while p.right is not None:
            p = p.right
        return p.key
```

---

## 이진 검색 트리 예시 코드

```Python
from enum import Enum

Menu = Enum("Menu", ["삽입", "삭제", "검색", "덤프", "키의범위", "종료"])

def select_Menu() -> Menu:
    s = [f"({m.value}){m.name}" for m in Menu]
    while True:
        print(*s, sep=" ", end=" ")
        n = int(input(": "))
        if 1 <= n <= len(Menu):
            return Menu(n)

tree = BinarySearchTree()

while True:
    menu = select_Menu()
    if menu == Menu.삽입:
        key = int(input("삽입할 키를 입력하세요.: "))
        val = input("삽입할 값을 입력하세요.: ")
        if not tree.add(key, val):
            print("삽입에 실패했습니다!")
    elif menu == Menu.삭제:
        key = int(input("삭제할 키를 입력하세요.: "))
        tree.remove(key)
    elif menu == Menu.검색:
        key = int(input("검색할 키를 입력하세요.: "))
        t = tree.search(key)
        if t is not None:
            print(f"이 키를 갖는 값은 {t}입니다.")
        else:
            print("해당하는 데이터가 없습니다.")
    elif menu == Menu.덤프:
        tree.dump()
    elif menu == Menu.키의범위:
        print(f"키의 최솟값은{tree.min_key()}입니다.")
        print(f"키의 최댓값은{tree.max_key()}입니다.")
    else:
        break
```