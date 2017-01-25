# 소개

프로그램을 유용하게 하기 위해서, 우리는 숫자, 문자열, 구조체, 논리값 등 가장 간단한 데이터 단위로 작업 할 수 있어야 합니다. TypeScript에서는 JavaScript에서 기대 할 수 있는 것과 함께 도움이 되도록 편리한 열거형을 지원 합니다.

# 논리형\(Boolean\)

가장 기본적인 자료형은 JavaScript와 TypeScript에서 `boolean`값 이라고 부르는, true/false 값 입니다.

```ts
let isDone: boolean = false;
```

# 숫자형\(Number\)

JavaScript 처럼 TypeScript의 모든 숫자는 부동소수점 값입니다. 이런 부동소수점 값들은 `number`자료형을 가집니다. TypeScript는 16진수 밎 10진수 표기법 외에도, ECMAScript 2015에 도입된 바이너리 밎 8진수를 지원합니다.

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

여러 줄과 embedded expressions을 가질 수 있는 _템플릿 문자열_ 또한 이용할 수 있습니다. 이런 문자열은 backtick/backquote \(`````````\) 문자로 둘러 쌓여 있으며, embedded expressions은`````${ expr }\`과 같은 형태로 되어 있습니다.

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

튜플 자료형은 요소의 개수와 자료형이 정해져 있는 배열을 표현 할 수 있습니다, 그러나 각 요소의 자료형이 같을 필요는 없습니다. 예를 들어, `string`과 `number` 쌍을 표현하고 싶다면:

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

`void` 형은 `any`형과 조금 반대됩니다: 어떠한 자료형도 가지지 않습니다. 여러분은 아마 일반적으로 반환 값이 없는 함수의 유형으로 이것을 볼 수 있을 것입니다 :

```ts
function warnUser(): void {
    alert("This is my warning message");
}
```

`void` 형의 변수를 선언하는 것은 유용하지 않습니다,  그 이유는 `undefined` 나 `null` 만 할당할 수 있기 때문입니다:

```ts
let unusable: void = undefined;
```

# Null과 Undefined

TypeScript에서, `undefined`와 `null` 은 실제로 가각  `undefined` 와 `null` 형을 가집니다. `void`와 매우 비슷하게, 그들 스스로는 매우 유용하지는 않습니다:

```ts
// 이 변수들에는 이 이값들 외에 할당할 수 있는 것이 별로 없습니다!
let u: undefined = undefined;
let n: null = null;
```

기본적으로 `null` 과 `undefined`는 모든 자료형의 하위 자료형입니다. 즉, `number` 같은 자료형에도`null` 과 `undefined` 를 할당 할 수 있습니다.

그러나, `--strictNullChecks` 플래그를 사용할 때는 `null` 과 `undefined는` `void` 와 해당 자료형에만 할당 할 수 있습니다. 이렇게 하면 _많은_ 일반적인 오류를 피할 수 있습니다. `string` 이나 `null` 이나 `undefined`을 전달하려는 경우,  여러분은 유니온 `string | null | undefined`자료형을 이용할 수 있습니다. 다시 한번 알려드립니다, 유니온 자료형에 대한 자세한 내용은 나중에 다루겠습니다.

> 참고 사항: 우리는 가능한 경우 `--strictNullChecks` 를 사용하는 것을 권장합니다, 그러나 이 핸드북의 목적 상 해제 되어 있다고 가정할 것입니다.

# Never

`never`형은 절대 발생하지 않는 값의 자료형을 나타냅니다. 예를 들어, `never` 는 반환 값이 없거나 항상 예외를 throw하는 함수 또는 화살표 함수표현\(arrow function expression\)의 반환형 입니다. 변수는 true가 아닌 유형의 가드에 의해 범위가 좁혀지면 `never` 형을 얻습니다.

`never` 형은 모든 자료형의 하위 자료형이며, 모든 자료형에 할당할 수 있습니다. 그렇지만, _아무_  자료형도`never` 의 하위 자료형이 아니며, 할당 할 수 없습니다\(`never` 자신은 제외\). `any` 조차도 `never`에 할당 할 수 없습니다.

`never`를 반환하는 함수의 몇가지 예:

```ts
// never를 반환하는 함수는 도달 할 수 없는 종점이 있어야 합니다
function error(message: string): never {
    throw new Error(message);
}

// 유추된 반환형은 X 입니다
function fail() {
    return error("Something failed");
}

// never를 반환하는 함수는 도달 할 수 없는 종점이 있어야 합니다
function infiniteLoop(): never {
    while (true) {
    }
}
```

# Type assertions

TypeScript를 사용하다보면 때로는 어떤 값에 대해 더 많은 가치를 알아야 할 상황에 처할 수 있습니다. 일반적으로 Type assertions은 어떤 entity의 유형을 현재 유형보다 더 구체적으로 표현할때 사용됩니다.

_Type assertions_은 컴파일러에게 "날 믿어, 난 내가 무슨일을 하고 있는지 알고 있어."라고 말하는 방법입니다.

Type assertion은 다른 언어들 에서의 형변환\(type cast\)과 비슷합니다, 그러나 특별한 검사를 하거나 데이터 재구성을 하지 않습니다. 이것은 런타임에는 영향을 미치지 않으며 컴파일러에서만 사용됩니다. TypeScript는 프로그래머가 필요한 특별한 검사를 수행했다고 가정합니다.

Type assertions 은 두가지 형식이 있습니다. 하나는 "angle-bracket" 문법 입니다:

```ts
let someValue: any = "this is a string";

let strLength: number = (<string>someValue).length;
```

다른 방법은 `as`-문법 입니다:

```ts
let someValue: any = "this is a string";

let strLength: number = (someValue as string).length;
```

두 샘플은 동일합니다. 둘중에 한가지를 고르는 것은 보통 취양에 따릅니다. 그러나, TypeScript를 JSX와 함께 사용할 때는, `as`-style assertions만 사용하실 수 있습니다.

# `let`에 관한 참고사항

알아차렸을지도 모르지만, 우리는 둘중에 아마도 더 친숙할 JavaScript의 `var`키워드 대신에 `let`을 사용하였습니다.`let`키워드는 TypeScript에서 이용가능한 실제 JavaScript 구문입니다.자세한 내용은 나중에 다루겠지만, `let`을 사용하면 JavaScript의 많은 일반적인 문제를 해결 할 수 있습니다, 따라서 가능하면 `var`대신 사용하기 바랍니다.

