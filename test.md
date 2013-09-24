<script>alert(test);</script>
##搜索结果 chunked 实验

###实验条件

* 没有连接wiaui(因为目前wiaui不支持chunked，同时带来的问题是无法压缩代码)
* 没有使用缓存
* 实验一：使用chunked模式，在请求odp的时候，首先下发搜索结果之前的代码，请求us之后，再下发结果页下面的代码
* 实验二：对照组同线上
* 实验一，二：query-快乐男声
* 实验三，四：query-test
* 实验一，二网络条件：Download/Upload bandwidth is 320000 bps 、Latency is 80 ms(因为没有使用缓存所以网速稍微快了一点)
* 实验三，四网络条件：wifi
* 实验次数 20
* 实验环境：PC

###实验一和实验二结果

`首字节时间`实验一：276ms 实验二：582ms <span style="color:green">306ms </span>

`us请求时间` 306ms

`top+head时间(实验一提前下发代码的时间)`实验一：360ms 实验二：363ms

`首屏渲染耗时`实验一：1022ms 实验二：1045ms <span style="color:red">23ms</span>

`实验三等待时间` 0ms

`首屏总时间` 实验一：1298ms 实验二：1627 <span style="color:green">329ms </span>

###实验三和实验四结果

`首字节时间`实验三：214ms 实验二：405ms <span style="color:green">191ms </span>

`us请求时间` 191ms

`top+head渲染时间(实验一提前下发代码的时间)`实验三：108ms 实验四：126ms

`首屏渲染耗时`实验三：148ms 实验四：146ms <span style="color:green">2ms</span>

`实验三等待时间` 191-108=83ms

`首屏总时间` 实验三：445ms 实验四：551ms <span style="color:green">106ms </span>

###实验总结
如果`us请求时间`>`top+head时间`，那么最终优化的时间是`top+head时间`

如果`us请求时间`<`top+head时间`,那么最终优化的时间是`us请求时间`

`us请求时间`相对比较稳定，而`top+head时间`是和网速成正相关的。所以如果网速非常快，`top+head时间`就会非常小，那么最终优化的结果就是`top+head时间`。

根据目前线上平均，使用chunked模式，大概可以优化200ms左右
