```python
# int
# float
# str
# bool

from typing import List, Dict, Tuple, \
    Set, Union, Optional, TypeVar, NewType, \
        TypedDict, Protocol, Awaitable, Callable, \
            Final, Literal, TypeGuard, Generic, ClassVar, NoReturn, Self, Iterable, Iterator, \
                AsyncIterator, Sequence, Coroutine, overload \
                

# List, Dict, Tuple, Set
numbers: List[int] = [1, 2, 3]
grades: Dict[str, float] = {"Alice": 90.5, "Bob": 82.3}
coordinates: Tuple[int, int] = (10, 20)
unique_ids: Set[int] = {1, 2, 3}

# Union
def process(value: Union[int, str]) -> None:
    print(value)
    
# Optional
def find_name(user_id: int) -> Optional[str]:
    if user_id == 1:
        return "Alice"
    return None


# Alias
Vector = List[float]

def add_vectors(v1: Vector, v2: Vector) -> Vector:
    return [x + y for x, y in zip(v1, v2)]

# Callable
def apply_function(func: Callable[[int, int], int], x: int, y: int) -> int:
    return func(x, y)

def add(a: int, b: int) -> int:
    return a + b

result = apply_function(add, 2, 3)

# Generic
T = TypeVar('T')



def get_first_element(elements: List[T]) -> T:
    return elements[0]

print(get_first_element([1, 2, 3]))  # int
print(get_first_element(["a", "b", "c"]))  # str



class TreeNode(Generic[T]):
    def __init__(self, value: T, left: Optional[TreeNode[T]] = None, right: Optional[TreeNode[T]] = None) -> None:
        self.value: T = value
        self.left: Optional[TreeNode[T]] = left
        self.right: Optional[TreeNode[T]] = right




T = TypeVar('T')

class Stack(Generic[T]):
    def __init__(self) -> None:
        self._items: List[T] = []

    def push(self, item: T) -> None:
        self._items.append(item)

    def pop(self) -> T:
        return self._items.pop()

stack = Stack[int]()
stack.push(1)
stack.push(2)
print(stack.pop())  # Output: 2


# NewType
UserId = NewType('UserId', int)

def get_user_name(user_id: UserId) -> str:
    return f"User {user_id}"

user_id = UserId(123)

# TypedDict
class Person(TypedDict):
    name: str
    age: int

person: Person = {"name": "Alice", "age": 30}

# Protocols
class Serializable(Protocol):
    def serialize(self) -> str:
        ...

class User:
    def serialize(self) -> str:
        return "user data"

def save_data(obj: Serializable) -> None:
    print(obj.serialize())

user = User()
save_data(user)

# Awaitable
async def fetch_data() -> str:
    return "data"

async def main() -> Awaitable[None]:
    data = await fetch_data()
    print(data)

# Coroutine - Coroutine[ReturnType, SendType, YieldType]
async def fetch_data() -> Coroutine[None, None, str]:
    await asyncio.sleep(1)
    return "data"


# AsyncIterator
async def generate_numbers(start: int, end: int) -> AsyncIterator[int]:
    for number in range(start, end):
        await asyncio.sleep(0)  # Simulate async work
        yield number

# Final
PI: Final = 3.14159  # This variable should not be changed

#Literal 
def process_color(color: Literal['red', 'green', 'blue']) -> None:
    if color == 'red':
        print("Processing red")
    elif color == 'green':
        print("Processing green")
    elif color == 'blue':
        print("Processing blue")

process_color('red')  # Valid
process_color('yellow')  # This will raise a type checker error

# TypeGuard
def is_list_of_strings(value: List[Union[int, str]]) -> TypeGuard[List[str]]:
    return all(isinstance(i, str) for i in value)

data: List[Union[int, str]] = ['a', 'b', 'c']
if is_list_of_strings(data):
    # Here, the type of data is narrowed to List[str]
    print(data)
    
# overload
@overload
def process(value: int) -> int:
    ...

@overload
def process(value: str) -> str:
    ...

def process(value):
    if isinstance(value, int):
        return value * 2
    elif isinstance(value, str):
        return value.upper()
    
# ClassVar
class MyClass:
    constant: ClassVar[int] = 10
    
# NoReturn
def fatal_error(message: str) -> NoReturn:
    raise RuntimeError(message)

# Self
class Node:
    def __init__(self, value: int) -> None:
        self.value = value
        self.next: Self = None

    def add(self, value: int) -> Self:
        self.next = Node(value)
        return self.next
    
    
# Iterable
def print_elements(elements: Iterable[int]) -> None:
    for element in elements:
        print(element)

print_elements([1, 2, 3])          # List
print_elements((4, 5, 6))          # Tuple
print_elements("hello")            # String

# Iterator
def get_squares(n: int) -> Iterator[int]:
    for i in range(n):
        yield i * i

squares = get_squares(5)
for square in squares:
    print(square)
    
# Sequence - фиксрованная длинна и доступ по индексу
def get_first_element(seq: Sequence[int]) -> int:
    return seq[0]

print(get_first_element([1, 2, 3]))  # List
print(get_first_element((4, 5, 6)))  # Tuple
```
