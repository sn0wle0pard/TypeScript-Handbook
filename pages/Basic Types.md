# 소개

프로그램을 유용하게 하기 위해, 우리는 숫자, 문자열, 구조체, 논리값 등 가장 간단한 데이터 단위로 작업 할 수 있어야 합니다. TypeScript에서는 JavaScript에서 기대 할 수 있는 것과 함께 도움이 되도록 편리한 열거형을 지원 합니다.

# 논리형\(Boolean\)

가장 기본적인 자료형은 JavaScript와 TypeScript에서 `boolean`값 이라고 부르는, true/false 값 입니다.

```ts
let isDone: boolean = false;
```

# 숫자형\(Number\)

JavaScript 처럼 TypeScript의 모든 숫자는 부동소수점 값입니다.  
이런 부동소수점 값들은 `number`자료형을 가집니다.  
TypeScript는 16진수 밎 10진수 표기법 외에도,  
ECMAScript 2015에 도입된 바이너리 밎 8진수를 지원합니다.

```ts
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
```

# 문자형\(String\)

웹 페이지와 서버의 JavaScript에서 프로그램을 생성하는 또 다른 기본적인 구성 요소는 텍스트 데이터와 함께 작업하는 것입니다. 다른 언어들과 마찬가지로, 우리는 문자형을 가리키기 위헤 `string`형식을 사용합니다. JavaScript와 마찬가지로 TypeScript도 큰 따옴표\(`"`\) 또는 \(`'`\)를 문자형 데이터를 감싸는데 이용합니다.

```ts
let color: string = "blue";
color = 'red';
```

여러 줄과 embedded expressions을 가질 수 있는 _템플릿 문자열_ 또한 이용할 수 있습니다.  
이런 문자열은 backtick/backquote \(``` ``\) 문자로 둘러 쌓여 있으며, embedded expressions은 `${ expr }`과 같은 형태로 되어 있습니다.

```ts
let fullName: string = `Bob Bobbington`;
let age: number = 37;
let sentence: string = `Hello, my name is ${ fullName }.

I'll be ${ age + 1 } years old next month.`
```

이는 이와 같은 `문장`을  선언하는 것과 같습니다:

```ts
let sentence: string = "Hello, my name is " + fullName + ".\n\n" +
"I'll be " + (age + 1) + " years old next month."
```

# 배열\(Array\)

TypeScript는 JavaScript처럼 배열을 사용할 수 있습니다.  
배열은 두가지 방법중 하나로 선언 할 수 있습니다.  
첫번째로, 요소의 자료형을 선언한 뒤 `[]`를 작성하여 해당 자료형의 배열을 선언합니다:

```ts
let list: number[] = [1, 2, 3];
```

두번째 방법은 `Array<elemType>`과 같은 제네릭 배열을 선언합니다:

```ts
let list: Array<number> = [1, 2, 3];
```

# 튜플\(Tuple\)

튜플 자료형은 요소의 개수와 자료형이 정해져 있는 배열을 표현 할 수 있습니다, 그러나 각 요소의 자료형이 같을 필요는 없습니다.  
예를 들어, `string`과 `number` 쌍을 표현하고 싶다면:

```ts
// 튜플 선언
let x: [string, number];
// 초기화
x = ["hello", 10]; // OK
// 잘못된 초기화
x = [10, "hello"]; // Error
```

알려진 인덱스가 있는 요소에 접근 할 때 올바른 유형이 검색됩니다:

```ts
console.log(x[0].substr(1)); // OK
console.log(x[1].substr(1)); // Error, 'number'형은 'substr'을 가지고 있지 않습니다
```

알려진 인덱스 집합 외부의 요소에 접근 할때는, 유니온\(union\) 자료형이 대신 이용 됩니다:

```ts
x[3] = "world"; // OK, 'string'형은 'string | number'에 접근 할 수 있습니다

console.log(x[5].toString()); // OK, 'string'과 'number'형은 둘다 'toString' 메소드를 가지고 있습니다

x[6] = true; // Error, 'boolean'형은 'string | number'형이 아닙니다
```

유니온\(Union\) 자료형은 추후에 다룰 고급 주제 입니다.

# 열거형\(Enum\)

`enum`은 JavaScript의 표준 자료형 모음에 추가된 유용한 자료형입니다. C\#같은 언어에서 처럼, 열거형은 친숙한 이름을 숫자값의 집합에 제공하는 방법입니다.

```ts
enum Color {Red, Green, Blue};
let c: Color = Color.Green;
```

기본적으로, 열거형은 `0`부터 시작하여 요소에 순서를 매깁니다. 요소 중 하나의 순서를 수동으로 변경할 수 있습니다.  
예를 들어, 위의 예제를 `0`대신에 `1`부터 시작하게 변경 할 수 있습니다:

```ts
enum Color {Red = 1, Green, Blue};
let c: Color = Color.Green;
```

또는 수동으로 열거형의 순서를 모두 설정 할 수 있습니다:

```ts
enum Color {Red = 1, Green = 2, Blue = 4};
let c: Color = Color.Green;
```

열거형의 편리한 기능으로 숫자값을 열거형 값의 이름으로 이동할 수 있습니다.  
예를 들어, 값이 `2`이지만 위의 `Color`열거형에 매핑 된 것이 확실하지 않은 경우 해당 이름을 찾을 수 있습니다:

```ts
enum Color {Red = 1, Green, Blue};
let colorName: string = Color[2];

alert(colorName);
```

# Any

프로그램을 작성할때 자료형을 모르는 변수를 선언할 필요가 있을 수 있습니다.이련 값들은 예를 들어 사용자나 서드파티 라이브러리에서 넘어오는 동적 컨텐트 일 수 있습니다. 이런 경우에, 우리는 타입 체킹을 생략하고, 컴파일 시간 동안 값을 통과 시키고 싶습니다. 그렇게 하기 위해서, 우리는 이것들을`any` 령으로 분류합니다:

```ts
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean
```

`any` 형은 기존의 자바스크립트와 함게 작업할 수 있는 강력한 방법이며, 컴파일 하는 중에 점진적으로 타입 체킹을 옵트인\(opt-in\)및 옵트아웃\(opt-out\)할 수 있습니다. 여러분은 다른 언어에서와 마찬가지로 `Object`가 비슷한 역할을 할 것으로 예상 하실 수 있습니다. 그러나 `Object` 유형으 변수는 값을 할당만 할 수 있습니다 - 실제로 존제하는 값이라도 임의의 메소드를 호출할 수는 없습니다:

```ts
let notSure: any = 4;
notSure.ifItExists(); // okay, 런타임에 ifItExists가 있을 수 있습니다
notSure.toFixed(); // okay, toFixed가 존재합니다 (그러나 컴파일러는 확인하지 않습니다)

let prettySure: Object = 4;
prettySure.toFixed(); // Error: Property 'toFixed' doesn't exist on type 'Object'.
```

`any`형은 일부 자료형을 알고 있으나 모든 자료형을 알고 있지 않을때도 편리합니다. 예를 들어, 여러분은 배열을 가지고 있지만 그 배열은 여러가지 다른 유형이 섞여 있을 수 있습니다:

```ts
let list: any[] = [1, true, "free"];

list[1] = 100;
```

# Void

`void` is a little like the opposite of `any`: the absence of having any type at all.  
You may commonly see this as the return type of functions that do not return a value:

```ts
function warnUser(): void {
alert("This is my warning message");
}
```

Declaring variables of type `void` is not useful because you can only assign `undefined` or `null` to them:

```ts
let unusable: void = undefined;
```

# Null과 Undefined

In TypeScript, both `undefined` and `null` actually have their own types named `undefined` and `null` respectively.  
Much like `void`, they're not extremely useful on their own:

```ts
// Not much else we can assign to these variables!
let u: undefined = undefined;
let n: null = null;
```

By default `null` and `undefined` are subtypes of all other types.  
That means you can assign `null` and `undefined` to something like `number`.

However, when using the `--strictNullChecks` flag, `null` and `undefined` are only assignable to `void` and their respective types.  
This helps avoid _many_ common errors.  
In cases where you want to pass in either a `string` or `null` or `undefined`, you can use the union type `string | null | undefined`.  
Once again, more on union types later on.

> As a note: we encourage the use of `--strictNullChecks` when possible, but for the purposes of this handbook, we will assume it is turned off.

# Never

The `never` type represents the type of values that never occur.  
For instance, `never` is the return type for a function expression or an arrow function expression that always throws an exception or one that never returns;  
Variables also acquire the type `never` when narrowed by any type guards that can never be true.

The `never` type is a subtype of, and assignable to, every type; however, _no_ type is a subtype of, or assignable to, `never` \(except `never` itself\).  
Even `any` isn't assignable to `never`.

Some examples of functions returning `never`:

```ts
// Function returning never must have unreachable end point
function error(message: string): never {
throw new Error(message);
}

// Inferred return type is never
function fail() {
return error("Something failed");
}

// Function returning never must have unreachable end point
function infiniteLoop(): never {
while (true) {
}
}
```

# Type assertions

Sometimes you'll end up in a situation where you'll know more about a value than TypeScript does.  
Usually this will happen when you know the type of some entity could be more specific than its current type.

_Type assertions_ are a way to tell the compiler "trust me, I know what I'm doing."  
A type assertion is like a type cast in other languages, but performs no special checking or restructuring of data.  
It has no runtime impact, and is used purely by the compiler.  
TypeScript assumes that you, the programmer, have performed any special checks that you need.

Type assertions have two forms.  
One is the "angle-bracket" syntax:

```ts
let someValue: any = "this is a string";

let strLength: number = (<string>someValue).length;
```

And the other is the `as`-syntax:

```ts
let someValue: any = "this is a string";

let strLength: number = (someValue as string).length;
```

The two samples are equivalent.  
Using one over the other is mostly a choice of preference; however, when using TypeScript with JSX, only `as`-style assertions are allowed.

# `let`에 관한 참고사항

알아차렸을지도 모르지만, 우리는 둘중에 아마도 더 친숙할 JavaScript의 `var`키워드 대신에 `let`을 사용하였습니다.  
`let`키워드는 TypeScript에서 이용가능한 실제 JavaScript 구문입니다.  
자세한 내용은 나중에 다루겠지만, `let`을 사용하면 JavaScript의 많은 일반적인 문제를 해결 할 수 있습니다, 따라서 가능하면 `var`대신 사용하기 바랍니다.

