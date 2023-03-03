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
```
class Resp {
    id: number;
    name: string;
}
class UserResponse extends Resp{
    registrationDate: string;
}
class AuthResponse extends Resp{
    avatar: string;
    login: string;
    user_token: string;
}
class Meta { }
class MetaTrackMessage extends Meta {
    trackId: string;
    trackerUrl: string
}
class LoadMetaMessage extends Meta {
    currentNodeId: string;
    currentNodeLoad: number;
}

class TResponse<TData, TMeta> {
    data: TData;
    meta: TMeta;
}

class SomeExternalApi {
    public static getUsers(): TResponse<Resp, Meta>[] {
        return [{
            data: new UserResponse(),
            meta: new MetaTrackMessage()
        },{
            data: new UserResponse(),
            meta: new LoadMetaMessage()
        },{
            data: new AuthResponse(),
            meta: new MetaTrackMessage()
        },{
            data: new UserResponse(),
            meta: new LoadMetaMessage()
        },{
            data: this.auth(),
            meta: new LoadMetaMessage()
        },]
    }

    public static auth(): AuthResponse {
        return {
            id: 124,
            avatar: "<http://llss.qiniudn.com/d234b75b6a7dfeda793b7da04a7c080dd.png>",
            name: "Johanna",
            login: "Johanna206",
            user_token: "eYEuVgUlDvRXgHR"
        }
    }
}
console.log(SomeExternalApi.getUsers());
```
# Задание 3. Классы
```
class MyArray<T> {
    private _elements: T[];
    private _length: number;

    constructor(array: T[] = []) {
        this._elements = array;
        this._length = this._elements.length;
    }

    get elements(): T[]{
        return this._elements;
    }
    set elements(value: T[]) {
        this._elements = value;
    }
    get length(): number {
        return this._length;
    }

    Copy(): Array<T> {
        let res: Array<T> = [];
        let length: number = 0;
        for(let e of this.elements) {
            res[length] = e;
            length++;
        }
        return res;
    }

    Push(...values: T[]): number {
        for (let v of values) {
            this.elements[this._length] = v;
            this._length++;
        }
        return this.length;
    }

    Concat(...arrays: Array<Array<T>>): Array<T> {
        let res: Array<T> = this.Copy()
        let length: number = res.length;
        for (let arr of arrays){
            for (let v of arr){
                res[length] = v;
                length++;
            }
        }
        return res;
    }

    Slice(start: number, end: number = this._length): Array<T>{
        if (!(start in this.elements && (end in this.elements || end === this._length)))
            throw new Error("Incorrect args.");

        let res: Array<T> = [];
        let resLength = 0;
        let ind = start;
        while(ind < end){
            res[resLength] = this.elements[ind];
            resLength++;
            ind++;
        }
        return res;
    }

    AreElementsEqual(ind1: number, ind2: number): boolean {
        if (!(ind1 in this.elements && ind2 in this.elements))
            throw new Error("IncorrectIndexes");

        let first = this.elements[ind1];
        let second = this.elements[ind2];
        if (typeof first === 'number' && typeof second === 'number' && isNaN(first))
            return isNaN(second);
        if (typeof first === 'object'){
            for (let key in first)
                if (!(second.hasOwnProperty(key) &&
                    (second[key] === first[key] || typeof second[key] === typeof first[key])))
                    return false;
            for (let key in second)
                if (!(first.hasOwnProperty(key) &&
                    (second[key] === first[key] || typeof second[key] === typeof first[key])))
                    return false;
            return true;
        }
        return this.elements[ind1] == this.elements[ind2];
    }

    Flatten(): Array<T>{
        return this.flattenArr(this.elements);
    }
    private flattenArr(array: Array<T>): Array<T>{
        let res: Array<T> = [];
        for (let v of array){
            if (Array.isArray(v)){
                res = this.customConcat(res, this.flattenArr(v));
            }
            else
                res[res.length] = v;
        }
        return res;
    }
    private customConcat(source: Array<T>, additional: Array<T>): Array<T> {
        let ind = 0;
        while(ind < additional.length){
            source[source.length] = additional[ind];
            ind++;
        }
        return source;
    }
}
```
Тесты
```

let a = new MyArray<number>()
let pushed = a.Push(1,2,3,4);
let concated = a.Concat([1,2],[1,1,1])
let sliced = a.Slice(2);
let sliced2 = a.Slice(2,3);
let equal = new MyArray<number>([NaN, NaN]).AreElementsEqual(0,1);
let equal1 = new MyArray<number>([1,2,1]).AreElementsEqual(0, 1);
let equal2 = new MyArray<number>([1,2,1]).AreElementsEqual(0, 2);
let equal3 = new MyArray<string>(["asd","asd"]).AreElementsEqual(0, 1);
let equal4 = new MyArray<{a:number, b:string}>([{a:10,b:"asd"},{a:10,b:"asd"}]).AreElementsEqual(0, 1);
let equal5 = new MyArray<{a:number[], b:{} , c: {a:number,b:string,c:{a:number}}}>([
    {a: [1,2,3], b: {}, c: {a:1,b:"asd", c: {a:-1}}},
    {a: [1,2,3], b: {}, c: {a:1,b:"asd", c: {a:1}}},
]).AreElementsEqual(0, 1);
let flatten = new MyArray<any>([[[[[[1]]]]],[[1]]]).Flatten();
```
