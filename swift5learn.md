# Swift5 学习笔记

## 基本知识

声明常量和变量

```swift
let maxmumNumberOfLoginAttempts = 10 //常量
var currentLoginAttempt = 0 //变量
```

声明类型

```swift
var welcomeMessage:String
welcomeMessage = "hello"
```

支持汉字

```swift
let 你好 = "你好世界"
```

打印,占位类似es6语法

```swift
print("the current value of friendlyWelcome is \(friendWelcome)")
```

可以不加冒号，建议加

Int,UInt 整型

Double,Float 浮点型

初次声明赋值类型

```swift
let meaningOfLife = 42
let pi = 3.14159
```

进制数

```swift
let decimalInterger = 17 //十进制
let binaryInteger = 0b10001 //二进制
let octalInteger = 0o21//八进制
let hexadecimalInteger = 0x11//16进制
```

进制扩展

```
1.25e2
0xFp-2
```

便于阅读

```swift
let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillon = 1_000_000.000_000_1
```

数字类型转换,位数限制

```swift
//超出范围
let cannotBeNegative:UInt8 = -1(error)
let tooBig:Int8 = Int8.max + 1(error)
//类型转换
let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
//整型转浮点
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
//浮点转整型
let integerPi = Int(pi)
```

类型别名

```swift
typealias AudioSample = UInt16

var maxAmplitudeFound = AudioSample.min
```

布尔值

```swift
let orangeAreOrange = true
```

元组(Tuples)

```swift
let http404Error = (404,"Not Found")
let (statusCode,statusMessage) = http404Error//es6的解构
print("The status code is \(statusCode)")
// Prints "The status code is 404"
print("The status message is \(statusMessage)")
// Prints "The status message is Not Found"

//下划线占位
let (justTheStatusCode, _) = http404Error
print("The status code is \(justTheStatusCode)")
//序号取值，类似数组
print("The status code is \(http404Error.0)")
// Prints "The status code is 404"
print("The status message is \(http404Error.1)")
// Prints "The status message is Not Found"
//单独命名
let http200Status = (statusCode: 200, description: "OK")
print("The status code is \(http200Status.statusCode)")
// Prints "The status code is 200"
print("The status message is \(http200Status.description)")
// Prints "The status message is OK"
```

可选（Optional）

```swift
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)//被推断为Int?

//nil的使用只有被声明为Optional的变量才可以
var serverResponseCode:Int? = 404
serverResponseCode = nil

var surveryAnswer:String?自动设为nil

```

可选绑定（Optional Binding）

```swift
if let actualNumber = Int(possibleNumber) {
    print("The string \"\(possibleNumber)\" has an integer value of \(actualNumber)")
} else {
    print("The string \"\(possibleNumber)\" could not be converted to an integer")
}

if let firstNumber = Int("4"), let secondNumber = Int("42"), firstNumber < secondNumber && secondNumber < 100 {
    print("\(firstNumber) < \(secondNumber) < 100")
}
// Prints "4 < 42 < 100"

if let firstNumber = Int("4") {
    if let secondNumber = Int("42") {
        if firstNumber < secondNumber && secondNumber < 100 {
            print("\(firstNumber) < \(secondNumber) < 100")
        }
    }
}

```

隐式解析可选类型（Implicitly Unwrapped Optionals）

```swift
//可选类型暗示了常量或者变量可以“没有值”。可选可以通过 if 语句来判断是否有值，如果有值的话可以通过可选绑定来解析值。有时候在程序架构中，第一次被赋值之后，可以确定一个可选类型总会有值。在这种情况下，每次都要判断和解析可选值是非常低效的，因为可以确定它总会有值。这种类型的可选状态被定义为隐式解析可选类型（implicitly unwrapped optionals）。把想要用作可选的类型的后面的问号（String?）改成感叹号（String!）来声明一个隐式解析可选类型当可选类型被第一次赋值之后就可以确定之后一直有值的时候，隐式解析可选类型非常有用。一个隐式解析可选类型其实就是一个普通的可选类型，但是可以被当做非可选类型来使用，并不需要每次都使用解析来获取可选值
let possibleString: String? = "An optional string."
let forcedString: String = possibleString! // 需要感叹号来获取值

let assumedString: String! = "An implicitly unwrapped optional string."
let implicitString: String = assumedString  // 不需要感叹号
//如果一个变量之后可能变成nil的话请不要使用隐式解析可选类型。如果你需要在变量的生命周期中判断是否是nil的话，请使用普通可选类型。
```

异常处理（Error Handling）

```swift
func canThrowAnError() throws {
    // this function may or may not throw an error
}

do{
  try canThrowError()
}catch{
  //error was thrown
}

unc makeASandwich() throws {
    // ...
}

do {
    try makeASandwich()
    eatASandwich()
} catch SandwichError.outOfCleanDishes {
    washDishes()
} catch SandwichError.missingIngredients(let ingredients) {
    buyGroceries(ingredients)
}

```



断言和先决条件(Assertions and Preconditions)

> 断言和先决条件发是运行时发生的检测。使用它们可以确保在执行后面的代码之前已经满足了条件。如果断言或者先决条件中的值是true，代码像原来一样继续执行。如果条件是false，程序当前的状态就是无效的，代码会结束执行，app也会停止运行。

```swift
let age = -3
assert(age >= 0, "A person's age can't be less than zero.")
// This assertion fails because -3 is not >= 0.

assert(age >= 0)

if age > 10 {
    print("You can ride the roller-coaster or the ferris wheel.")
} else if age >= 0 {
    print("You can ride the ferris wheel.")
} else {
    assertionFailure("A person's age can't be less than zero.")
}

precondition(index > 0, "Index must be greater than zero.")
```

