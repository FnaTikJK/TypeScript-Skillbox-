# Задание 1. Работа с функцией
```
function arrayDiff(a: number[], b: number[]): number[] {
    return a.filter(e => b.indexOf(e) === -1);
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
function capitalizeLine(line: string): string{
    return line.split(' ')
                .map(s => s && s[0].toUpperCase() + s.slice(1))
                .join(' ');
}
```
# Задание 4. Массивы (часть 2)
```
function capitalizeLine(line: string): string{
    let reversed = line.split(' ')
                        .map(s => s && s[0].toUpperCase() + s.slice(1));
    reversed.splice(reversed[0].length, 1)
    return reversed.join(' ');
}
```
# Задание 5. Объекты v2 — код
```
function areEqual(a: object, b: object): boolean{
    return JSON.stringify(a) === JSON.stringify(b);
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
