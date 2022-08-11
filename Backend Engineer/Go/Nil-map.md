### Nil map

Acessing a nil map is OK, but storing a nil map cause program panic:

```
var m map[int]bool
	fmt.Println(" m is a nil? ", m == nil)
	fmt.Println("m[1] is ", m[1])
	m[1] = true

>> m isa nil? true
>> error: panic: assignment to entry in nil map
```

So the best practice is to initialize a map before using it, like this:

```
m := make(map[int]bool)
```

Should use to check

```
if v, ok := m[1]; !ok {
	.....
}

```
