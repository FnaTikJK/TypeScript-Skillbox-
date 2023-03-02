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

```
