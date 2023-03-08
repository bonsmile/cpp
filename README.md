# cpp
C++ Coding Style

## C++ 标准

使用 C++20 标准

## 排版和命名

一、入乡随俗，保持一致性



## auto 的使用

允许使用的场景：
* 模板类型（拼写较长）

## 字符串

## 文件 IO



## 数据结构

### 顺序容器

在选择数据结构时应优先考虑 std::vector, std::array 这类顺序容器，他们天然是缓存友好的。

### 关联容器

使用 `phmap::flat_hash_map/set` 替代 `std::unordered_map/set`; 

默认 `btree_map/set` 替代 `std::map/set`, 但有[两种意外](https://abseil.io/about/design/btree)：

* 当关联容器里面需要存储的值的长度大于 std::array<int32_t, 16> 时
* 插入/删除一个对象需要保证指向其他对象指针不失效
