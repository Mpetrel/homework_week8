### Redis 测试

#### 1. Set, Get 测试
10 20 50 100 200 1k 5k

| 数据字节 |  get  |  set  |
| :----: | :----: | :----: |
| 10   | 101010.10 requests per second, p50=0.255 msec | 101010.10 requests per second, p50=0.255 msec |
| 20   | 113636.37 requests per second, p50=0.231 msec | 114942.53 requests per second, p50=0.215 msec |
| 50   | 151515.16 requests per second, p50=0.191 msec | 113636.37 requests per second, p50=0.223 msec |
| 100  | 107526.88 requests per second, p50=0.239 msec | 125000.00 requests per second, p50=0.255 msec |
| 200  | 107526.88 requests per second, p50=0.239 msec | 149253.73 requests per second, p50=0.231 msec |
| 1024 | 144927.55 requests per second, p50=0.279 msec | 108695.65 requests per second, p50=0.231 msec |
| 5120 | 131578.95 requests per second, p50=0.231 msec | 114942.53 requests per second, p50=0.223 msec |

#### 2. 内存大小
> 使用 ` redis-benchmark -n 10000 -d 1024 -r 10000000 -t set -q` 随机插入 10000条数据，指定大小为1K

写入1000条数据， value大小1kb
写入前 `used_memory_dataset = 41640`
写入后 `used_memory_dataset = 13075296`

减去value占用内存 `1024 * 10000` ,平均每个key占用约283字节