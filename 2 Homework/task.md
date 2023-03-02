# Задание 1. Работа с функцией
```
function ArrayDiff(a: number[], b: number[]): number[] {
    let res: number[] = [];
    for(let e of a) {
        if (b.indexOf(e) === -1)
            res.push(e)
    }
    return res;
}
```
# Задание 2. Объединение типов + массивы
```
const arr1: number[] = [1, 2, 3, null];
const arr2: (string | boolean)[] = ['safety', '=', true]
const arr3: (number[] | string[]) [] = [
    [1, 2, 3, 4, 5],
    ['1', '2', '3', '4', '5'],
]
const arr4: (string | number | boolean)[] = [
    1, 2, true, 'str', undefined
]

const arr5: { id: number, name: string }[] = [
    {
        id: 1,
        name: 'Студент',
    },
    {
        id: 2,
        name: 'Наставник',
    }
]
```
# Задание 3. Массивы (часть 1)
```
function CapitalizeLine(line: string): string{
    let res: string[] = [];
    line.split(' ')
        .forEach(e =>
            res.push(CapitalizeWord(e)));
    return res.join(" ");
}

function CapitalizeWord(s: string): string
{
    return s && s[0].toUpperCase() + s.slice(1);
}
```
# Задание 4. Массивы (часть 2)
```
function CapitalizeLine(line: string): string{
    let res: string[] = [];
    let indToDelete: number;
    line.split(' ')
        .forEach((value, index) =>{
            if (index === 0)
                indToDelete = value.length;
            if (index === indToDelete)
                return;
            res.push(CapitalizeWord(value))
        });
    return res.join(" ");
}

function CapitalizeWord(s: string): string
{
    return s && s[0].toUpperCase() + s.slice(1);
}
```
# Задание 5. Объекты v2 — код
```
function AreEqual(a: object, b: object): boolean{
    for (var key in a) {
        if (!b.hasOwnProperty(key) || b[key] !== a[key])
            return false;
    }
    for (var key in b) {
        if (!a.hasOwnProperty(key) || b[key] !== a[key])
            return false;
    }
    return true;
}
```
# Задание 6. Community (часть 1)
```
export type User = {
    name: string,
    age: number,
    occupation: string
};
export const users: User[] = [
    {
        name: 'Roman Abramov',
        age: 25,
        occupation: 'Millionaire'
    },
    {
        name: 'Andrey Fox',
        age: 23,
        occupation: 'Developer'
    }
];
export function logPerson(user: User) {
    console.log(` - ${user.name}, ${user.age}`);
}
console.log('Users:');
users.forEach(logPerson);
```
# Задание 7. Community (часть 2)
```
type User = {
    name: string;
    age: number;
    occupation: string;
}
type Admin = {
    name: string;
    age: number;
    role: string;
}
export type Person = User | Admin;
export const persons: Person[] = [
    {
        name: 'Roman Abramov',
        age: 25,
        occupation: 'Millionaire'
    },
    {
        name: 'Jane Doe',
        age: 32,
        role: 'Administrator'
    },
    {
        name: 'Andrey Fox',
        age: 23,
        occupation: 'Developer'
    },
    {
        name: 'Bruce Willis',
        age: 64,
        role: 'World saver'
    }
];
export function logPerson(user: Person) {
    console.log(` - ${user.name}, ${user.age}`);
}
persons.forEach(logPerson);
```
