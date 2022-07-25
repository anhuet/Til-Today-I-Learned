## What are chanels

Chanels can be through of as pipes using with Goroutines communicate. Data can be sent from one and received frpm the other and using chanels

## Declaring channels

```
var a chan int
```

Short hande declaration:

```
a:= make(chan int)
```

## Sending and receiving from a channel

```
data := <- a // read from channel a
```

```
a <- data // write data to channel a
```

<strong>Note: Sends and receives are blocking by default. It's mean when data sent to chanel, the control block in the send statement util some other Goroutine read from channel and vice versa </strong>

### Examples

```
package main

import (
    "fmt"
)

func hello(done chan bool) {
    fmt.Println("Hello world goroutine")
    done <- true
}
func main() {
    done := make(chan bool)
    go hello(done)
    <-done // block when data sent into done
    fmt.Println("main function")
}
>> Hello world goroutine
>> main function

```

### Deadlock

```
package main


func main() {
    ch := make(chan int)
    ch <- 5
}
```

If a Goroutine is sending data on a channel, then it is expected that some other Goroutine should be receiving the data. If this does not happen, then the program will panic at runtime with Deadlock.
