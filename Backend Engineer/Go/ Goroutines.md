### What is the goroutines

Goroutines are functions or methods that run concurrently with other functions or methods.

### Advantages of Goroutines over threads

- Goroutines are extremely cheap ~ few kb in stack size
- The Goroutines are multiplexed to a fewer number of OS threads. There might be only one thread in a program with thousands of Goroutines.
- Goroutines communicate using channels. Channels by design prevent race conditions from happening when accessing shared memory using Goroutines.

### Example

#### Create a goroutines

```
package main

import {
    "fmt"
}

func hello() {
    fmt.Println("Hello, world!");
}

func main() {
    go hello();
    fmt.Println("Main thread");
}

>> Main thread
```

** Not wait for the Goroutine to finish excuting, return next line immediately without any value are returned **

Fix that:

```
package main

import {
    "fmt"
    "time"
}

func hello() {
    fmt.Println("Hello, world!");
}

func main() {
    go hello();
    time.Sleep(1 * time.Second)
    fmt.Println("Main thread");
}

>> Hello, world!
>> Main thread
```

** Now the main goroutine is sleeping for 1s, enough time to hello() to execute before the main Goroutine terminates **

Multi goroutines

```
package main

import (
    "fmt"
    "time"
)

func numbers() {
    for i := 1; i <= 5; i++ {
        time.Sleep(250 * time.Millisecond)
        fmt.Printf("%d ", i)
    }
}
func alphabets() {
    for i := 'a'; i <= 'e'; i++ {
        time.Sleep(400 * time.Millisecond)
        fmt.Printf("%c ", i)
    }
}
func main() {
    go numbers()
    go alphabets()
    time.Sleep(3000 * time.Millisecond)
    fmt.Println("main terminated")
}
>> 1 a 2 3 b 4 c 5 d e main terminated
```
