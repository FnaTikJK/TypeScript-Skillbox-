# Задание 1. Функции
```
type Obj = {
    age: number;
}

type Person = Obj & {
    name: string
}
type Bridge = Obj & {
    city: string
}
type Wine = Obj & {
    manufacturer: string,
    grade: string
}
function getOldestObj<T extends Obj>(items: T[]): T {
    return items.sort((a, b) => b.age - a.age)[0];
}

let oldestPerson: Person = getOldestObj([{age:10, name:"10"}, {age:1, name:"1"}])
let oldestBridge: Bridge = getOldestObj([{age:10, city:"10"}, {age:1, city:"1"}])
let oldestWine: Wine = getOldestObj([{age:10, manufacturer:"10", grade:"asd"}, {age:1, manufacturer:"1", grade:"рпва"}])
```
# Задание 2. Типы

# Задание 3. Классы
