# rwlock-go

###使用方式

``` 
go get github.com/wangfeiso/rwlock
```

###快速使用

```
import (
	"github.com/wangfeiso/rwlock"
)

func main() {
    
    // init your redis client
    // 目前仅仅支持单机
    rwlock.Init(&rwlock.Options{
        Addr: "127.0.0.1:6379",
    })
    
    //开始使用分布式读写锁
    
    //创建一个锁
    lock := rwlock.New("YourLockKey")
    
    // 加上写锁
    lock.Lock()
    
    // 释放写锁
    lock.Unlock()
    
    // 加上读锁
    lock.RLock()
    
    // 释放读锁
    lock.RUnlock()
    
}

```

### 说明
读写锁之间的互斥性如下

| 互斥性 | 读锁 | 写锁 |
| :-----| ----: | :----: |
| 读锁 | 兼容 | 互斥 |
| 写锁 | 互斥 | 互斥 |

读锁与写锁不能同时存在，读锁和读锁可以同时存在