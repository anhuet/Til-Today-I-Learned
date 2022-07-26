### What are buffered channels?

Buffered channels can be created by passing an additional capacity parameter to the make function which specifies the size of the buffer.

```
ch := make(chan type, capacity) // capacity > 0
```

<strong>Sends to a buffered channel are blocked only when the buffer is full. Similarly receives from a buffered channel are blocked only when the buffer is empty</strong

### Examples

```
package main
import (
    "fmt"
)
func main() {
    ch = make(chan string, 2)
    ch <-'vla'
    ch <- 'andy'
    fmt.Println(<-ch)
    fmt.Println(<-ch)
}
>> vla
>> any
```

```
package main

import (
    "fmt"
    "time"
)

func write(ch chan int) {
    for i := 0; i < 5; i++ {
        ch <- i
        fmt.Println("successfully wrote", i, "to ch")
    }
    close(ch)
}
func main() {
    ch := make(chan int, 2)
    go write(ch)
    time.Sleep(2 * time.Second)
    for v := range ch {
        fmt.Println("read value", v,"from ch")
        time.Sleep(2 * time.Second)

    }
}
>> successfully wrote 0 to ch
>> successfully wrote 1 to ch
>> read value 0 from ch
>> successfully wrote 2 to ch
>> read value 1 from ch
>> successfully wrote 3 to ch
>> read value 2 from ch
>> successfully wrote 4 to ch
>> read value 3 from ch
>> read value 4 from ch
```

### Deadlock

Write 3 string to buffered channel of capacity 2

```
package main

import (
    "fmt"
)

func main() {
    ch := make(chan string, 2)
    ch <- "naveen"
    ch <- "paul"
    ch <- "steve"
    fmt.Println(<-ch)
    fmt.Println(<-ch)
}

```
