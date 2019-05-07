## 如何使用redis

### redis 常见数据类型

- String (字符串)

```
SET name value

GET name
```

- Hash (哈希 键值对)

```
HMSET myhash field1 "Hello" field2 "World"

HGET myhash field1
```

- List (列表)

```
LPUSH lists one
LPUSH lists two
LPUSH lists three

LRANGE lists 0 10
```

- Set (集合)

```
sadd sets one
sadd sets two
sadd sets three
sadd sets four

smembers sets
```
