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
