# @lru\_cache

* lru\_cache - 함수의 반환값을 기억해줌. `lru_cache`는 데코레이터로 사용되는데, 원하는 함수에 이 데코레이터를 달아 주면 반환값을 알아서 저장해준다.

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fibo(n):
    if n < 2:
        return n
    return fibo(n - 1) + fibo(n - 2)

print(fibo(int(input())))
```
