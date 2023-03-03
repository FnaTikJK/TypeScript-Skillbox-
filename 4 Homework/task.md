# Задание 1. Классы/модификаторы/статические
```
type IUser = {
    messages: number,
    warnings: number;
    registration: Date
}

class TrustedUser {
    constructor(public readonly User: IUser) {
    }

    GetConfidenceRatio(): number {
        return this.User.messages * 2 - this.User.warnings * 100
            + (new Date()).getDay() - this.User.registration.getDay();
    }
}

class ConfidenceHelper {
    static IsReliableUser(user: TrustedUser): boolean { /// Переименовал, тк по семантике метода название от скиллбокса не подходит
        return user.GetConfidenceRatio() >= 0;
    }
}

function GetUnreliableUsers(users: TrustedUser[], checkerFunc: (user: TrustedUser) => boolean): TrustedUser[]{
    return users.filter(e => !checkerFunc(e));
}
```
Работу алгоритма можно проверить на этих данных
```
let users: TrustedUser[] = [new TrustedUser({
    messages: 100, warnings: 0, registration: new Date()
}), new TrustedUser({
    messages: 0, warnings: 1, registration: new Date()
}), new TrustedUser({
    messages: 99, warnings: 1, registration: new Date("2020-01-01")
})]

let unreliable = GetUnreliableUsers(users, ConfidenceHelper.IsReliableUser);
```
# Задание 2. Наследование/абстрактные/гетсет
1 Разработайте базовый класс Product, описывающий товар.
```
class Product extends ILogged{
    private _name: string;
    private _priceInRub: number;

    constructor(name:string, priceInRub: number) {
        super();
        this.name = name;
        this.priceInRub = priceInRub;
    }
    get name(): string {
        return this._name;
    }
    set name(value: string) {
        if (value.length > 0)
            this._name = value;
    }
    get priceInRub(): number {
        return this._priceInRub;
    }
    set priceInRub(value: number) {
        if (value > 0)
            this._priceInRub = value;
    }
}
```
Реализовал log() в классе-родителе, тк он универсален для всех
```
class ILogged {
    log(){
        console.log((Object.getOwnPropertyNames(this)
            .map(prop => typeof this[prop]['log'] === 'function' ?
                this[prop].log()
                : `${prop}: ${this[prop]}`))
            .join(";"));
    }
}
```
2 Разработайте абстрактный базовый класс AbstractPurchase, описывающий покупку товара.
```
abstract class AbstractPurchase extends ILogged {
    private _product: Product;
    private _amount: number;

    constructor(product: Product, amount: number) {
        super();
        this.product = product;
        this.amount = amount;
    }
    get product(): Product {
        return this._product;
    }
    set product(value: Product) {
        this._product = value;
    }
    get amount(): number {
        return this._amount;
    }
    set amount(value: number) {
        if (value >= 0)
            this._amount = value;
    }

    abstract GetCost(): number;

    Compare(other: AbstractPurchase): number{
        return other.GetCost() - this.GetCost();
    }
}
```
3 Реализуйте первый производный класс от AbstractPurchase, в котором продажа товара осуществляется со скидкой от цены. Переопределите нужные методы.
```
class DiscountPurchase extends AbstractPurchase {
    constructor(product: Product, amount: number) {
        super(product, amount);
    }

    GetCost(): number {
        return this.product.priceInRub * this.amount * 0.9;
    }
}
```
4 Реализуйте второй производный класс от AbstractPurchase, в котором скидка присутствует, если количество единиц товара не меньше некоторого числа, заданного константой в классе. Переопределите нужные методы.
```
class ConditionedDiscountPurchase extends AbstractPurchase{
    private readonly minimalAmount: number;

    constructor(product: Product, amount:number, minimalAmount: number) {
        super(product, amount);
        this.minimalAmount = minimalAmount;
    }

    GetCost(): number {
        let discount = this.amount >= this.minimalAmount ? 0.1 : 0;
        return this.product.priceInRub * this.amount * (1-discount);
    }
}
```
5 Реализуйте третий производный класс от AbstractPurchase, в котором к стоимости товара добавляются дополнительные транспортные расходы. Переопределите и добавьте нужные методы.
```
class PurchaseWithTransportationCost extends AbstractPurchase {
    private _transportationCost: number;

    constructor(product: Product, amount: number, transportationCost: number) {
        super(product, amount);
        this.transportationCost = transportationCost;
    }

    get transportationCost(): number{
        return this._transportationCost;
    }
    set transportationCost(value: number){
        if (value >= 0)
            this._transportationCost = value;
    }

    GetCost(): number {
        return (this.product.priceInRub + this._transportationCost) * this.amount;
    }
}
```
6 Реализуйте приложение, в котором:
Создайте массив из шести объектов (по два для каждого производного класса).
Выведите объекты в терминал через log*()*.
Отсортируйте объекты по убыванию с использованием метода Array.sort().
Выведите объекты в терминал.
```
let array: AbstractPurchase[] = [ /// Последняя цифра в названии продукта - итогая стоимость покупки. Для того чтобы сверить сортировку
    new DiscountPurchase(new Product("1-1 180", 100), 2),
    new DiscountPurchase(new Product("1-2 135", 150), 1),
    new ConditionedDiscountPurchase(new Product("2-1 181.8", 101), 2, 2),
    new ConditionedDiscountPurchase(new Product("2-2 202", 101), 2, 3),
    new PurchaseWithTransportationCost(new Product("3-1 501", 1), 1, 500),
    new PurchaseWithTransportationCost(new Product("3-2 400", 200), 2, 0)
]


array.forEach(e => e.log());
array = array.sort((a, b) => a.Compare(b));
console.log();
console.log("Отсортированные")
array.forEach(e => e.log());
```
