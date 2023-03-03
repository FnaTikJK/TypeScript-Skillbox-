# Задание 1. Pick, Exclude
```
type MyOmit<T, K> = Pick<T, Exclude<keyof T, K>>
```
# Задание 2.  Простой собственный тип 
```
type First<T extends [...T]> = T[0];
```
# Задание 3. Omit, Readonly
```
type MyReadonly<T, K extends keyof T = keyof T> = T & {
    readonly [P in K]: T[P];
};
```
# Задание 4. DeepReadonly
```
type DeepReadonly<T extends {}> = {readonly [P in keyof T]: DeepReadonly<T[P]> };
```
