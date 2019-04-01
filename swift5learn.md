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

## 基本运算符

+，-，*，/，%

```swift
"hello" + "world" //加号支持字符串连接
```

二目运算符

```
-=,+=,*=,
```

比较运算符

```
==,!=,>,<,>=,<=
```

元组之间的比较类似字符串比较大小

```swift
(1, "zebra") < (2, "apple")   // true because 1 is less than 2; "zebra" and "apple" are not compared
(3, "apple") < (3, "bird")    // true because 3 is equal to 3, and "apple" is less than "bird"
(4, "dog") == (4, "dog")      // true because 4 is equal to 4, and "dog" is equal to "dog"

布尔值之间不能比较
```

三目运算符

```
?:
```

空合运算符(Nil-Coalescing Operator)

> 空合运算符（a??b）将对可选类型a进行空判断,如果a包含一个值就进行解封，否则就返回一个默认值b，这个运算符有两个条件
>
> . 表达式a 必须是optional类型
>
> .默认值b的类型必须要和a存储值的类型保持一致

```
a != nil ? a! : b
```

区间运算符（Range Operators)

```swift
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}

```

半开区间运算符

```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
let count = names.count
for i in 0..<count {
    print("Person \(i + 1) is called \(names[i])")
}

```

单侧区间运算符

```swift
let numbers = [1,2,3,4,5,6,7,8,9,10]
numbers[5...] // instead of numbers[5..<numbers.endIndex]

for name in names[2...] {
    print(name)
}
    // Brian
    // Jack

for name in names[...2] {
    print(name)
}
    // Anna
    // Alex
    // Brian
for name in names[..<2] {
    print(name)
}
// Anna
// Alex

```

逻辑运算符

```
!,&&,||
```

## 字符串和字符

```swift
let someString = "Some string literal value"
```

多行字符串

```swift
let quotation = """
The White Rabbit put on his spectacles.  "Where shall I begin,
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on
till you come to the end; then stop."
"""
```

特殊字符

```swift
let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
// "Imagination is more important than knowledge" - Einstein
let dollarSign = "\u{24}"        // $,  Unicode scalar U+0024
let blackHeart = "\u{2665}"      // ♥,  Unicode scalar U+2665
let sparklingHeart = "\u{1F496}" // 💖, Unicode scalar U+1F496

```

扩展字符分割

```swift
    let threeMoreDoubleQuotationMarks = #"""
    Here are three more double quotes: """
    """#

```

初始化空字符串

```swift
var emptyString = ""               // empty string literal
var anotherEmptyString = String()  // initializer syntax

//判断字符串是否为空
if emptyString.isEmpty {
    print("Nothing to see here")
}
// Prints "Nothing to see here"

```

可变字符串与不可变字符串

```swift
var variableString = "Horse"
variableString += " and carriage"
// variableString is now "Horse and carriage"

let constantString = "Highlander"
constantString += " and another Highlander"
// this reports a compile-time error - a constant string cannot be modified

```

字符

```swift
for character in "Dog!🐶" {
    print(character)
}
// D
// o
// g
// !
// 🐶
//初始化字符
let exclamationMark: Character = "!"
//字符组装字符串
let catCharacters: [Character] = ["C", "a", "t", "!", "🐱"]
let catString = String(catCharacters)
print(catString)
// Prints "Cat!🐱"

let string1 = "hello"
let string2 = " there"
var welcome = string1 + string2

let exclamationMark: Character = "!"
welcome.append(exclamationMark)
```

字符串插入

```swift
let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
// message is "3 times 2.5 is 7.5"
print(#"Write an interpolated string in Swift using \(multiplier)."#)
// Prints "Write an interpolated string in Swift using \(multiplier)."

```

字符个数

```swift
let unusualMenagerie = "Koala 🐨, Snail 🐌, Penguin 🐧, Dromedary 🐪"
print("unusualMenagerie has \(unusualMenagerie.count) characters")
// Prints "unusualMenagerie has 40 characters"

```

字符索引

相当于把字符当数组来处理了

```swift
let greeting = "Guten Tag!"
greeting[greeting.startIndex]
// G
greeting[greeting.index(before: greeting.endIndex)]
// !
greeting[greeting.index(after: greeting.startIndex)]
// u
let index = greeting.index(greeting.startIndex, offsetBy: 7)
greeting[index]
// a

for index in greeting.indices {
    print("\(greeting[index]) ", terminator: "")
}

// Prints "G u t e n   T a g ! "
```

插入删除

```swift
var welcome = "hello"
welcome.insert("!", at: welcome.endIndex)
// welcome now equals "hello!"

welcome.insert(contentsOf: " there", at: welcome.index(before: welcome.endIndex))
// welcome now equals "hello there!"

welcome.remove(at: welcome.index(before: welcome.endIndex))
// welcome now equals "hello there"

let range = welcome.index(welcome.endIndex, offsetBy: -6)..<welcome.endIndex
welcome.removeSubrange(range)
// welcome now equals "hello"

```

字符串截取

```
let greeting = "Hello, world!"
let index = greeting.firstIndex(of: ",") ?? greeting.endIndex
let beginning = greeting[..<index]
// beginning is "Hello"

// Convert the result to a String for long-term storage.
let newString = String(beginning)
```

字符串相等

```
let quotation = "We're a lot alike, you and I."
let sameQuotation = "We're a lot alike, you and I."
if quotation == sameQuotation {
    print("These two strings are considered equal")
}
// Prints "These two strings are considered equal" 
```

前缀后缀

```swift
let romeoAndJuliet = [
    "Act 1 Scene 1: Verona, A public place",
    "Act 1 Scene 2: Capulet's mansion",
    "Act 1 Scene 3: A room in Capulet's mansion",
    "Act 1 Scene 4: A street outside Capulet's mansion",
    "Act 1 Scene 5: The Great Hall in Capulet's mansion",
    "Act 2 Scene 1: Outside Capulet's mansion",
    "Act 2 Scene 2: Capulet's orchard",
    "Act 2 Scene 3: Outside Friar Lawrence's cell",
    "Act 2 Scene 4: A street in Verona",
    "Act 2 Scene 5: Capulet's mansion",
    "Act 2 Scene 6: Friar Lawrence's cell"
]
var act1SceneCount = 0
for scene in romeoAndJuliet {
    if scene.hasPrefix("Act 1 ") {
        act1SceneCount += 1
    }
}
print("There are \(act1SceneCount) scenes in Act 1")

```

## 集合类型

### 数组

创建空数组

```swift
var someInts = [Int]()
print("someInts is of type [Int] with \(someInts.count) items.")
// Prints "someInts is of type [Int] with 0 items."

someInts.append(3)
// someInts now contains 1 value of type Int
someInts = []
// someInts is now an empty array, but is still of type [Int]
```

创建带初始值的数组

```swift
var threeDoubles = Array(repeating: 0.0, count: 3)
// threeDoubles is of type [Double], and equals [0.0, 0.0, 0.0]

```

两个数组相加

```
var anotherThreeDoubles = Array(repeating: 2.5, count: 3)
// anotherThreeDoubles is of type [Double], and equals [2.5, 2.5, 2.5]

var sixDoubles = threeDoubles + anotherThreeDoubles
// sixDoubles is inferred as [Double], and equals [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]
```

逐个创建

```swift
var shoppingList: [String] = ["Eggs", "Milk"]
// shoppingList has been initialized with two initial items
var shoppingList = ["Eggs", "Milk"]
```

查询和修改一个数组

```swift
print("The shopping list contains \(shoppingList.count) items.")
// Prints "The shopping list contains 2 items."
```

判断数组是否为空

```swift
if shoppingList.isEmpty {
    print("The shopping list is empty.")
} else {
    print("The shopping list is not empty.")
}
// Prints "The shopping list is not empty."
```

添加数组元素

```swift
shoppingList.append("Flour")
// shoppingList now contains 3 items, and someone is making pancakes
```

数组使用数学运算符

```swift
shoppingList += ["Baking Powder"]
// shoppingList now contains 4 items
shoppingList += ["Chocolate Spread", "Cheese", "Butter"]
// shoppingList now contains 7 items
```

索引取值

```swift
var firstItem = shoppingList[0]
// firstItem is equal to "Eggs"

```

索引赋值

```swift
shoppingList[0] = "Six eggs"
// the first item in the list is now equal to "Six eggs" rather than "Eggs"
```

插入元素

```swift
shoppingList.insert("Maple Syrup", at: 0)
// shoppingList now contains 7 items
```

删除元素

```swift
let mapleSyrup = shoppingList.remove(at: 0)
// the item that was at index 0 has just been removed
```

遍历数组

```swift
for item in shoppingList {
    print(item)
}
// Six eggs
// Milk
// Flour
// Baking Powder
// Bananas

for (index, value) in shoppingList.enumerated() {
    print("Item \(index + 1): \(value)")
}
// Item 1: Six eggs
// Item 2: Milk
// Item 3: Flour
// Item 4: Baking Powder
// Item 5: Bananas
```

### 集合

初始化空集合

```swift
var letters = Set<Character>()
print("letters is of type Set<Character> with \(letters.count) items.")
// Prints "letters is of type Set<Character> with 0 items."

letters.insert("a")
// letters now contains 1 value of type Character
letters = []
// letters is now an empty set, but is still of type Set<Character>
```

使用数组初始化一个集合

```swift
var favoriteGenres: Set<String> = ["Rock", "Classical", "Hip hop"]
// favoriteGenres has been initialized with three initial items

var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]
```

查询和修改一个集合

```swift
print("I have \(favoriteGenres.count) favorite music genres.")
// Prints "I have 3 favorite music genres."

//判断集合是否为空
if favoriteGenres.isEmpty {
    print("As far as music goes, I'm not picky.")
} else {
    print("I have particular music preferences.")
}
//插入一个集合元素
favoriteGenres.insert("Jazz")
// favoriteGenres now contains 4 items

//移除一个集合元素
if let removedGenre = favoriteGenres.remove("Rock") {
    print("\(removedGenre)? I'm over it.")
} else {
    print("I never much cared for that.")
}

//检查元素是否被集合包含
if favoriteGenres.contains("Funk") {
    print("I get up on the good foot.")
} else {
    print("It's too funky in here.")
}

```

遍历集合

```swift
for genre in favoriteGenres {
    print("\(genre)")
}
// Classical
// Jazz
// Hip hop

//集合排序
for genre in favoriteGenres.sorted() {
    print("\(genre)")
}
// Classical
// Hip hop
// Jazz
```

两个集合之间的运算

```swift
a.intersection(b)//交集
a.symmetricDifference(b)//并集减去交集
a.union(b)//并集
a.subtracting(b)//a-a交b
```

两个集合之间的关系

```swift
let houseAnimals: Set = ["🐶", "🐱"]
let farmAnimals: Set = ["🐮", "🐔", "🐑", "🐶", "🐱"]
let cityAnimals: Set = ["🐦", "🐭"]

houseAnimals.isSubset(of: farmAnimals)
// true
farmAnimals.isSuperset(of: houseAnimals)
// true
farmAnimals.isDisjoint(with: cityAnimals)
// true
```

### 字典

创建一个空字典

```swift
var namesOfIntegers = [Int: String]()
// namesOfIntegers is an empty [Int: String] dictionary

namesOfIntegers[16] = "sixteen"
// namesOfIntegers now contains 1 key-value pair
namesOfIntegers = [:]
// namesOfIntegers is once again an empty dictionary of type [Int: String]
```

初始化一个字典

```swift
var airports: [String: String] = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]

var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
```

查询和修改一个字典

```swift
print("The airports dictionary contains \(airports.count) items.")
// Prints "The airports dictionary contains 2 items."

//判断字典是否为空
if airports.isEmpty {
    print("The airports dictionary is empty.")
} else {
    print("The airports dictionary is not empty.")
}
//元素赋值
airports["LHR"] = "London"
// the airports dictionary now contains 3 items
//元素改值
airports["LHR"] = "London Heathrow"

if let oldValue = airports.updateValue("Dublin Airport", forKey: "DUB") {
    print("The old value for DUB was \(oldValue).")
}
// Prints "The old value for DUB was Dublin."

//根据key取值
if let airportName = airports["DUB"] {
    print("The name of the airport is \(airportName).")
} else {
    print("That airport is not in the airports dictionary.")
}
//删除键值对
airports["APL"] = "Apple International"
// "Apple International" is not the real airport for APL, so delete it
airports["APL"] = nil
// APL has now been removed from the dictionary

if let removedValue = airports.removeValue(forKey: "DUB") {
    print("The removed airport's name is \(removedValue).")
} else {
    print("The airports dictionary does not contain a value for DUB.")
}
```

遍历一个字典

```swift
for (airportCode, airportName) in airports {
    print("\(airportCode): \(airportName)")
}
// YYZ: Toronto Pearson
// LHR: London Heathrow

for airportCode in airports.keys {
    print("Airport code: \(airportCode)")
}
// Airport code: YYZ
// Airport code: LHR

for airportName in airports.values {
    print("Airport name: \(airportName)")
}
// Airport name: Toronto Pearson
// Airport name: London Heathrow

//取所有的键值导出数组
let airportCodes = [String](airports.keys)
// airportCodes is ["YYZ", "LHR"]

let airportNames = [String](airports.values)
// airportNames is ["Toronto Pearson", "London Heathrow"]

```

## 控制流

### For循环

```swift
//数组
let names = ["Anna", "Alex", "Brian", "Jack"]
for name in names {
    print("Hello, \(name)!")
}
// Hello, Anna!
// Hello, Alex!
// Hello, Brian!
//字典（es6的解构）
let numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
for (animalName, legCount) in numberOfLegs {
    print("\(animalName)s have \(legCount) legs")
}
// ants have 6 legs
// cats have 4 legs
// spiders have 8 legs

//区间运算符
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25

//不需要索引，使用下划线占位
let base = 3
let power = 10
var answer = 1
for _ in 1...power {
    answer *= base
}
print("\(base) to the power of \(power) is \(answer)")

//单侧区间运算符
let minutes = 60
for tickMark in 0..<minutes {
    // render the tick mark each minute (60 times)
}

//抽稀
let minuteInterval = 5
for tickMark in stride(from: 0, to: minutes, by: minuteInterval) {
    // render the tick mark every 5 minutes (0, 5, 10, 15 ... 45, 50, 55)
}

```

### While循环

```swift
while condition {
     statements
}

repeat {
    statements
} while condition
```

### 条件语句

```swift
//if
temperatureInFahrenheit = 90
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    print("It's really warm. Don't forget to wear sunscreen.")
} else {
    print("It's not that cold. Wear a t-shirt.")
}

//switch
let someCharacter: Character = "z"
switch someCharacter {
case "a":
    print("The first letter of the alphabet")
case "z":
    print("The last letter of the alphabet")
default:
    print("Some other character")
}
//区间匹配

et approximateCount = 62
let countedThings = "moons orbiting Saturn"
let naturalCount: String
switch approximateCount {
case 0:
    naturalCount = "no"
case 1..<5:
    naturalCount = "a few"
case 5..<12:
    naturalCount = "several"
case 12..<100:
    naturalCount = "dozens of"
case 100..<1000:
    naturalCount = "hundreds of"
default:
    naturalCount = "many"
}
print("There are \(naturalCount) \(countedThings).")
// Prints "There are dozens of moons orbiting Saturn."

//元组匹配
let somePoint = (1, 1)
switch somePoint {
case (0, 0):
    print("\(somePoint) is at the origin")
case (_, 0):
    print("\(somePoint) is on the x-axis")
case (0, _):
    print("\(somePoint) is on the y-axis")
case (-2...2, -2...2):
    print("\(somePoint) is inside the box")
default:
    print("\(somePoint) is outside of the box")
}
//值绑定
let anotherPoint = (2, 0)
switch anotherPoint {
case (let x, 0):
    print("on the x-axis with an x value of \(x)")
case (0, let y):
    print("on the y-axis with a y value of \(y)")
case let (x, y):
    print("somewhere else at (\(x), \(y))")
}
// Prints "on the x-axis with an x value of 2"

//where
let yetAnotherPoint = (1, -1)
switch yetAnotherPoint {
case let (x, y) where x == y:
    print("(\(x), \(y)) is on the line x == y")
case let (x, y) where x == -y:
    print("(\(x), \(y)) is on the line x == -y")
case let (x, y):
    print("(\(x), \(y)) is just some arbitrary point")
}
// Prints "(1, -1) is on the line x == -y"

//合成
let someCharacter: Character = "e"
switch someCharacter {
case "a", "e", "i", "o", "u":
    print("\(someCharacter) is a vowel")
case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
     "n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
    print("\(someCharacter) is a consonant")
default:
    print("\(someCharacter) is not a vowel or a consonant")
}
// Prints "e is a vowel"

```

控制转移语句

```

 continue
 break
 fallthrough//成功了继续执行下一个case
 return
 throw

```

带标签的语句

> 在`swift`中，你可以在循环体或者`switch`代码块中嵌套循环体和`switch`代码块来创造复杂的控制流结构，然而，循环体和switch代码块两者都可以使用`break`语句来提前结束整个方法体，因此，显式的指明`break`语句想要终止的是哪个循环体或者`switch`代码块，会很有用。

```swift
lable name : while condition {

      statements
}
var number = 10
    whilLoop : while number > 0 {

        switch number {
        case 9:
            print("9")
        case 10:
            var sum = 0
            for index in 0...10 {
                sum += index
                print(sum)
                if index == 9 {
                    break whilLoop
                }
            }
        default:
            break;
        }
        number -= 1
    }
```

## 函数