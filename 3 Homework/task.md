# Задание 1. Приведение типов (as)
```
function getHouse(): House {
    return {
        street: 'Pushkina',
        apartmentCount: 76,
        buildInfo: {
            year: 1996,
            material: 'rocks',
        }
    }
}
```
Ошибка была из-за того что мы обращаемся к неинициализированным полям, тк соверашем плохое приведение типов. Исправить можно возвращая сразу нужный объект или указав ему нужный тип самостоятельно.
# Задание 2. Тайпгарды + объединение
Обычные тайпгарды
```
if(IsCat(pet))
    return (pet as Cat).meow();
if(IsDog(pet))
    return (pet as Dog).bark();
```
Кастомные
```
function IsCat(pet: Cat | Dog): boolean{
    return pet.hasOwnProperty('meow');
}
function IsDog(pet: Cat | Dog): boolean{
    return pet.hasOwnProperty('bark');
}
```
Через in
```
if ('meow' in pet)
    return pet.meow();
if ('bark' in pet)
    return pet.bark();
```
# Задание 3. Перечисления
```
enum Directions {
    Up,
    Down,
    Left,
    Right
}
type Player = {
    x: number,
    y: number,
    move: (direcion: Directions, amount: number) => void,
}
const player: Player = {
    x: 0,
    y: 0,
    move: function (direction: Directions, amount: number) {
        switch (direction) {
            case Directions.Up:
                this.y += amount;
                break;
            case Directions.Down:
                this.y -= amount;
                break;
            case Directions.Left:
                this.x -= amount;
                break;
            case Directions.Right:
                this.x += amount;
                break;
            default:
                break;
        }
    }
}
player.move(Directions.Up, 1);
player.move(Directions.Down, 2);
player.move(Directions.Left, 2);
player.move(Directions.Right, 3);
console.log(player.x === 1); // true
console.log(player.y === -1); // true
```
Enum делает код более чиатбельным.
# Задание 4. Community (часть 3)
