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
