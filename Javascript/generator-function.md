# Generator Function
The function* defines a *generator function,* which return a **Generator** object

>function* generator(i) {
> yield i;
> yield i + 10;
>}
>
>const gen = generator(10);
>
>console.log(gen.next().value);
>// expected output: 10
>
>console.log(gen.next().value);
>// expected output: 20

Generators are functions that can be exited and later re-entered. Their context (variable bindings) will be saved across re-entrances.

>function* idMaker() {
> var index = 0;
>  while (true)
>    yield index++;
>}
>
> var gen = idMaker();
>
>console.log(gen.next().value); // 0
>console.log(gen.next().value); // 1
>console.log(gen.next().value); // 2
>console.log(gen.next().value); // 3