# syncmap

add length func base on go 1.9 sync.map .  from : https://github.com/rfyiamcool/syncmap

引于： https://github.com/rfyiamcool/syncmap ，因这块直接调用Length时，int64指针没有生成，会异常，所以稍加改动。

Golang官方在 1.9 加入了sync.map协程安全的map, 性能和安全得以保证，就是没有Length方法. 自己丰衣足食加了个补丁.

至于官方为什么不加Length方法原因，有兴趣的可以看看issue. 简单说官方认为 map 本来就不应该有length的实现.


#How

在sync.map结构体里加了计数器，在触发Store和Delete时，Atomic.AddInit64 +1 -1就可以了.
