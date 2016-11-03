转载来自http://foofish.net/blog/92/python_dict_implements

字典类型是Python中最常用的数据类型之一，它是一个键值对的集合，字典通过键来索引，关联到相对的值，理论上它的查询复杂度是 O(1) ：

PyDictObject对象就是dict的内部实现。

## PyDictEntry

字典中的一个key-value键值对元素称为entry（也叫做slots），对应到Python内部是PyDictEntry，PyDictObject就是PyDictEntry的集合。PyDictEntry的定义是：

    typedef struct {
        /* Cached hash code of me_key.  Note that hash codes are C longs.
         * We have to use Py_ssize_t instead because dict_popitem() abuses
         * me_hash to hold a search finger.
         */
        Py_ssize_t me_hash;
        PyObject *me_key;
        PyObject *me_value;
    } PyDictEntry;

me_hash用于缓存me_key的哈希值，防止每次查询时都要计算哈希值，entry有三种状态。

- Unused： me_key == me_value == NULL
    - Unused是entry的初始状态，key和value都为NULL。插入元素时，Unused状态转换成Active状态。这是me_key为NULL的唯一情况。
- Active： me_key != NULL and me_key != dummy 且 me_value != NULL
    - 插入元素后，entry就成了Active状态，这是me_value唯一不为NULL的情况，删除元素时Active状态刻转换成Dummy状态。
- Dummy： me_key == dummy 且 me_value == NULL
    - 此处的dummy对象实际上一个PyStringObject对象，仅作为指示标志。Dummy状态的元素可以在插入元素的时候将它变成Active状态，但它不可能再变成Unused状态。
    
为什么entry有Dummy状态呢？这是因为采用开放寻址法中，遇到哈希冲突时会找到下一个合适的位置，例如某元素经过哈希计算应该插入到A处，但是此时A处有元素的，通过探测函数计算得到下一个位置B，仍然有元素，直到找到位置C为止，此时ABC构成了探测链，查找元素时如果hash值相同，那么也是顺着这条探测链不断往后找，当删除探测链中的某个元素时，比如B，如果直接把B从哈希表中移除，即变成Unused状态，那么C就不可能再找到了，因为AC之间出现了断裂的现象，正是如此才出现了第三种状态---Dummy，Dummy是一种类似的伪删除方式，保证探测链的连续性。