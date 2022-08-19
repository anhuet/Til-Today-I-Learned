### What is the closures
A closure is a function that references variables outside of its scope which it is created It can access variables within that scope, even after the scope is destroyed.

E.g: 
```
package main

import "fmt"

func closureFn() func() int {
	i := 0
	return func() int {
		i++
		return i
	}

}
func main() {
    temp := closureFn()

	for i := 0; i < 3; i++ {
		fmt.Printf("%d ,", temp());
	}
} 
>> 1,2,3 
```