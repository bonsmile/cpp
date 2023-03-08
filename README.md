# cpp
C++ Coding Style

## 现代 C++ 最佳实践

### auto 的使用
`auto` 很多时候被滥用了，我们允许使用的场景：
* 模板类型（拼写较长）

例如

## 错误和异常处理
Bad:
```
bool loadBonMAndBonS_win32(ArrayView<const char> bonm, ArrayView<const char> bons, Vector2i size) {
    _scene.reset(new bon::Scene());
    if(_scene->loadBonMAndBonS(bonm, bons, size)) {
        _scene->resize(windowSize());
        return true;
    }

    _scene.reset();
    return false;
}
```
Good:
```
bool loadBonMAndBonS_win32(ArrayView<const char> bonm, ArrayView<const char> bons, Vector2i size) {
    _scene.reset(new bon::Scene());
    // 错误处理在前
    if(!_scene->loadBonMAndBonS(bonm, bons, size)) {
        _scene.reset();
        return false;
    }
    // 成功操作在后
    _scene->resize(windowSize());
    return true;
}
```
## 排版和命名

一、入乡随俗，保持一致性





## 字符串

## 文件 IO

### 打开文件

### 将文件读取到字符串

### 

## 数据结构

### 顺序容器

在选择数据结构时应优先考虑 std::vector, std::array 这类顺序容器，他们天然是缓存友好的。

### 关联容器

使用 `phmap::flat_hash_map/set` 替代 `std::unordered_map/set`; 

默认 `btree_map/set` 替代 `std::map/set`, 但有[两种意外](https://abseil.io/about/design/btree)：

* 当关联容器里面需要存储的值的长度大于 std::array<int32_t, 16> 时
* 插入/删除一个对象需要保证指向其他对象指针不失效
