## 3.1 Partial, Required, Readonly, Pick, Record

기존 객체의 속성을 전부 옵션으로 만드는 Partial 타입

```ts
type MyPartial<T> = {
  [P in keyof T]?: T[P];
};

type Result = MyPartial<{ a: string, b: number }>;

/*
type Result = {
  a?: string | undefined;
  b?: number | undefined;
}
*/
```

모든 속성을 필수로 만드는 Required 타입

```ts
type MyRequired<T> = {
  [P in keyof T]-?: T[P];
};

type Result = MyRequired<{ a?: string, b?: number }>;

/*
type Result = {
  a: string;
  b: number;
}
*/
```

모든 속성을 readonly나 readonly가 아니게 만드는 Readonly 타입

```ts
type MyReadonly<T> = {
  readonly [P in keyof T]: T[P];
};

type Result = MyReadonly<{ a: string, b: number }>;

/*
type Result = {
  readonly a: string;
  readonly b: number;
}
*/

type MyNotReadonly<T> = {
  -readonly [P in keyof T]: T[P];
};

type Result2 = MyNotReadonly<Result>

/*
type Result2 = {  
  a: string;  
  b: number;  
}
*/
```

객체에서 지정한 속성만 추리는 Pick 타입

```ts
type MyPick<T, K extends keyof T> = {
  [P in K]: T[P];
};

type Result = MyPick<{ a: string, b: number, c: number }, 'a' | 'c'>;

/*
type Result = {
  a: string;
  c: number;
}
*/
```

모든 속성의 타입이 동일한 Record 타입

```ts
type MyRecord<K extends keyof any, T> = {
  [P in K]: T;
};

type Result = MyRecord<'a' | 'b', string>;

/*
type Result = {
  a: string;
  b: string;
}
*/
```
## 3.2 Exclude, Extract, Omit, NonNullable

지정한 타입을 제거하는 Exclude 타입

```ts
type MyExclude<T, U> = T extends U ? never : T;
type Result = MyExclude<1 | '2' | 3, string>;
// type Result = 1 | 3
```

지정한 타입만 추출하는 Extract 타입

```ts
type MyExtract<T, U> = T extends U ? T : never;
type Result = MyExtract<1 | '2' | 3, string>;
// type Result = "2"
```

지정한 속성을 제거하는 Omit 타입
 - Exclude를 이용해 지정한 속성을 제거하고 Pick 타입으로 추려낸 속성을 선택

```ts
type MyOmit<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>;
type Result = MyOmit<{ a: '1', b: 2, c: true }, 'a' | 'c'>;
// type Result = { b: 2 }
```

null과 undefined를 제거하는 NonNullable 타입

```ts
type MyNonNullable<T> = T extends null | undefined ? never : T;
type Result = MyNonNullable<string | number | null | undefined>;
// type Result = string | number

type MyNonNullable<T> = T & {};
```

일부 속성만 옵셔널로 만드는 옵셔널 타입
 - 옵셔널이 될 속성을 Pick으로 골라서 Partial을 적용하고 아닌 속성들은 Omit으로 추려 & 연산자로 합침

```ts
type Optional<T, K extends keyof T> = Omit<T, K> & Partial<Pick<T, K>>

type Result = Optional<{ a: 'hi', b: 123 }, 'a'>;
// type Result = { a?: 'hi', b: 123 }
```
## 3.3 Parameters, ConstructorParameters, ReturnType, InstanceType

```ts
type MyParameters<T extends (...args: any) => any>
  = T extends (...args: infer P) => any ? P : never;

type MyConstructorParameters<T extends abstract new (...args: any) => any>
  = T extends abstract new (...args: infer P) => any ? P : never;

type MyReturnType<T extends (...args: any) => any>
  = T extends (...args: any) => infer R ? R : any;

type MyInstanceType<T extends abstract new (...args: any) => any>
  = T extends abstract new (...args: any) => infer R ? R : any;
```

## 3.4 ThisType

메서드들에 this를 주입하는 타입

```ts
type Data = { money: number };
type Methods = {
  addMoney(amount: number): void;
  useMoney(amount: number): void;
};
type Obj = {
  data: Data;
  methods: Methods & ThisType<Data & Methods>;
};
const obj: Obj = {
  data: {
    money: 0,
  },
  methods: {
    addMoney(amount) {
      this.money += amount;
    },
    useMoney(amount) {
      this.money -= amount;
    }
  }
};
```

아래 구문 실행 시 money 값이 변경되지 않음

```ts
obj.methods.addMoney(10)
console.log(obj.data)

// { "money": 0 }
```

## 3.5 forEach 만들기

## 3.6 map 만들기

## 3.7 filter 만들기

## 3.8 reduce 만들기

## 3.9 flat 분석하기

## 3.10 Promise, Awaited 타입 분석하기

## 3.11 bind 분석하기