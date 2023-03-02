# Задание 1. Ошибка в коде (1)

```
const actor = {
    name: 'Michael',
    firstName: 'Ivanov',
    country: 'Russia',
    city: 'Machachkala',
    hasOskar: false,
    filmsCount: 10,
    age: '14',
    languages: ['RU-ru', 'EN-us', 'TR-tr'],
};
const howOldWillBeActorAfterTwentyYears = (actor) => {
    return actor.age + 20;
}
console.log(howOldWillBeActorAfterTwentyYears(actor)); // '1420'
```
Ответ: Программа выдаёт 1420 тк у поля age объекта actor стоит неправильный тип данных и ts складывает их как строки. Необходимо поменять строку
```
age: '14',
```
на 
```
age: 14,
```
# Задание 2. Ошибка в коде (2)
```
document.addEventListener('click', (e) => {
    const coords = [e.posX, e.posY];
    console.log(`Point is ${coords[0]}, ${coords[1]}`);
});
```
ошибка возникла из-за того, что объект e не имеет таких полей как posX и posY. Нужно заглянуть в документацию и найти нужные поля
```
const coords = [e.posX, e.posY];
```
заменить на
```
const coords = [e.x, e.y];
```
# Задание 3. Использование нетипизированного кода
```
function someFunc(data) {
  return data.reduce((acc, current) => {
        acc + Number(current.age > 18 && current.isMale), 0);
    };
}
```
Код, по идее, вообще не скомпилируется, тк написан неправильно. Но я предполагаю, что он ведёт счёт и увеличивает счётчик если ему подали объект с полями age и isMale и они удовлетворяют определённым условиям
```
type Human = {
    name: string,
    age: number,
    gender: 'male' | 'female',
}
function someFunc(data: Human[]): number {
  return data.reduce((acc: number, current: Human) => {
        acc + Number(current.age > 18 && current.gender === 'male'), 0);
    };
}
```
Код опять не скомпилируется, но здесь уже более явная реализация, что именно считает программа - кол-во мужчин в возрасте старше 18 лет.

# Задание 4. Написание кода
```
function GetPartialReversedString(line: string){
    let res: string = "";
    for (let s of line.split(' '))
        res += reverse(s) + " ";
    return res;
}

# Пришлось написать кастомный ревёрс строки (в шоке что тут его нет)
function reverse(s){
    return s.split("").reverse().join("");
}
```


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

```
function GetDigitalSum(numb: number): number {
    let sum: number = 0;
    while(numb>0){
        sum += numb % 10;
        numb = Math.floor(numb/10);
    }
    return sum < 10 ? sum
        : GetDigitalSum(sum);
}
```
