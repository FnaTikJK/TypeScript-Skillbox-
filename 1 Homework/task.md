# Задание 1. Ошибка в коде (1)

# Задание 2. Ошибка в коде (2)

# Задание 3. Использование нетипизированного кода

# Задание 4. Написание кода

# Задание 5. Алгоритмическая задача (1)

```
#Функция-ответ задачи
function GetSquaredDigits(numb:number) : number {
    if (numb<0)
        return numb;
    let numbers: number[] = Digitize(numb);
    let res: string = "";
    for(let n of numbers){
        res += (n * n).toString();
    }
    return Number(res);
}

#Разбивает число на массив цифр
function Digitize(numb: number): number[] { 
    let answer: number[] = [];
    while(numb > 0){
        answer.push(numb % 10);
        numb = Math.floor(numb/10);
    }
    return answer.reverse();
}
```

# Задание 6. Алгоритмическая задача (2)
