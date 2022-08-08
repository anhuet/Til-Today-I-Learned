### What is select
The <strong>Select </strong> statement is used to choose from multi send/recieve channel operations.
Block until one of the send/recieve operarion is ready and random chosen one of them when they ready
Similar switch statement except that case will be a channle operation

### Example

```
func server1(ch chan string) {
    time.Sleep(6 * time.Second)
    ch <- "from server1"
}
func server2(ch chan string) {
    time.Sleep(3 * time.Second)
    ch <- "from server2"

}
func main() {
    output1 := make(chan string)
    output2 := make(chan string)
    go server1(output1)
    go server2(output2)
    select {
    case s1 := <-output1:
        fmt.Println(s1)
    case s2 := <-output2:
        fmt.Println(s2)
    }
}
>> from server2
server1 sleeps for 6s
server2 sleeps for 3s
the select block until one of its case is ready
server 1 write ouput 1 after 6s
server 2 wirte output 2 after 3s
so the select will block 3s and w print output 2
```
