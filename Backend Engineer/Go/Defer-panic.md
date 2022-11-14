### What is defer
A defer statement defers the execution of a function until the surrounding function returns

<strong> Note : The deferred call's arguments are evaluated immediately but the function is not executed until the surrounding function returns </strong>    

After defer keyword always a function

```
func main() {
	defer fmt.Print("world")

	fmt.Print("hello")
}
>> hello world
```

Stack defer
```
func main() {
	defer fmt.Print("1")
  defer fmt.Print("2")
  defer fmt.Print("3")
}
>> 3 2 1
```
```
func main() {
  a := 12
  defer fmt.Print(a)
  a = 24
}
>> 12
```

### What is panic
Panic is a built-in function that stops the ordinary flow of control and begins panicking.

```
func main() {
  a:= 10
  b:= 0
  panic("divide a number by 0")
  fmt.Print(a / b)
}
>> panic: divide a number by 0
>> erorr
```

### Handle panic with defer and recover

```
fmt.Println("Start ")
    defer func() {
        if err := recover(); err != nil {
            fmt.Println("Error", err)
        }
	}()
	panic("will throw a panic")
	fmt.Println("End")
```