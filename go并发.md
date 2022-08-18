
在 Go 的标准库中，package sync 提供了锁相关的一系列同步原语，这个package还定义了一个Locker的接口，Mutex就实现了这个接口。

## Mutex

Mutex 是go官方提供的互斥锁，它提供了两个方法 Lock 和 Unlock：进入临界区之前调用Lock方法，退出临界区的时候调用Unlock方法。我们可以使用互斥锁，限定临界区只能同时有一个线程持有。

![图 1](images/dff2c400e3c4d966c02527884e7a38f5ec494b2ef6449a78ea2d50f6e40f2b57.png)  

当一个goroutine通过调用Lock方法获得了这个锁的拥有权后，其他请求锁的goroutine就会阻塞在Lock方法的调用上，直到锁被释放并且自己获取到了这个锁的拥有权。

**临界区**

在并发编程中，如果程序中的一部分会被并发访问或修改，那么，为了避免并发访问导致的意想不到的结果，这部分程序需要保护起来的程序，就叫做临界区

**例子**

```go
type Counter struct {
	CounterType int
	Name        string

	mu    sync.Mutex
	count uint64
}

func (c *Counter) Incr() {
	c.mu.Lock()
	c.count++
	c.mu.Unlock()
}
func (c *Counter) Count() uint64 {
	c.mu.Lock()
	defer c.mu.Unlock()
	return c.count
}

func mutex() {
	var counter Counter
	var wg sync.WaitGroup
	wg.Add(10)
	for i := 0; i < 10; i++ {
		go func() {
			defer wg.Done()
			for j := 0; j < 100000; j++ {
				counter.Incr()
			}
		}()
	}
	wg.Wait()
	fmt.Println(counter.Count())
}
```