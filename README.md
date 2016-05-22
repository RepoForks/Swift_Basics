##イントロ
これはswiftの基本をおさえるためのノートです。
このガイドは素早くわからないところを確認するために使用してください。より深い内容を理解したい場合は以下の公式のドキュメントを確認してください。
*このドキュメントはプログラミングを始めて学ぶ人に向けた内容となっています。

* [WWDC 2014: Introduction to Swift](https://developer.apple.com/videos/wwdc/2014/#402)
* [iOS Developer Library: A Swift Tour](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/GuidedTour.html)
* [iBooks: The Swift Programming Language](https://itunes.apple.com/us/book/swift-programming-language/id881256329)


##宣言について(Declarations)
### letとvarについて
`let`は定数(constant)。`var`は変数(variable)の宣言に使用します。変数とは宣言した値を後で変更することができるものです。(他にも細かい違いはありますが、最初は深く考えすぎないように！)


```swift
var mutableNumber = 0
mutableNumber = mutableNumber + 1 // 変数varはあとで値を変更できる

let immutableNumber = 0
immutableNumber = immutableNumber + 1 // 定数letはあとで値を変更できない
```

### 型(Type)
```swift
let i: Int = 0
```
"定数iはInt型"
左から右に読みましょう(Javaとは逆なんで気持ち悪いですねw)


但しSwiftには、型を自動的に推測する機能が備わっています。上でみたように型が明らかな場合は型宣言を省略することができます。

```swift
let i = 0
```

また、タイプエイリアス(typealias)とは、型の別名定義のことです。
Swiftでは、C言語のtypedefのように、既存の型に別名をつけて使用することができます。

```swift
typealias StatusCode = Int
let okResponse: StatusCode = 200
```


##プリミティブ(基本的な型について)
###Strings
```swift
let name = "太郎"
let interpolatedString = "Hello \(name)"    // "Hello 太郎"
let concatenatedString = "Hello" + " world" // "Hello world"
```
###Numbers
```swift
let myNumber = 27                     // Intになる
let myFloat: Float = 27               // Floatになる
let floatConversion = Float(myNumber) // myNumberがFloatに変換される
```

###Bool
論理型は（true）か（false）の２値をとる型で、Boolで指定します。Falseは0,空の文字列,nilとは別です。

```swift
var answer: Bool
let myTrueValue = true
let myFalseValue = false
```

###配列(Arrays)
```swift
let myArray = ["Red", "Orange", "Yellow"]
```
基本的にArrayは一つの型しか含むことができません。さらに配列に含むものの型を以下のように指定することもできます。

```swift
let myArray : [String] = ["Red", "Orange", "Yellow"]
```

空の配列を宣言するときは以下のように記述できます。

```swift
var myEmptyArray = [String]()
myEmptyArray.append("Red")
```


###ディクショナリ(Dictionaries)
ディクショナリは、文字列や数値をキーにして値を格納したり参照できる型です。

```swift
let characterDictionary = ["America": "Washington, D.C.", "Japan": "Tokyo"]
```

同様に空のディクショナリは以下のように宣言し、値を挿入します。

```swift
var characterDictionary: [String:String] = Dictionary<String, String>()
characterDictionary["Simba"] = "Matthew Broderick"
```

###タプル(Tuples)
タプルは、複数の値を一組にしたものです。配列と似ていますが、配列と違って異なる型の値をまとめることができます。但し、後から要素を追加したり削除することはできません。

```swift
let myColors = ("Green", "Blue", "Indigo", "Violet")
println(myColors.2) // "Indigo"
```
以下のような使い方をすると便利ですね。

```swift
let myResponse: (code: Int, message: String) = (200, "OK")
println(myResponse.message)
```

## 制御文(Control Flow)

### If



```swift
if 条件1 {
    条件1がtrueの場合に実行する処理
} else if 条件2 {
    条件2がtrueの場合に実行する処理
  :
} else {
    上のどの条件にも合致しなかった場合に実行する処理
}
```
`Bool`のみが条件として利用できます。`0`と`1`はboolean型とは別です。

```swift
if numberValue == 1 {
  println("The value was 1.")
}
```

### Switch
switch文を使うと、値に応じた処理内容を記述することができます。値のパターンが多い場合、if文を使うより見通しよく書けます。C言語やJavaのswitch文と似ていますが、Swiftのswitch文はより柔軟な比較判定が可能です。

```swift
switch someValue {
   case 1:
     println("Hit single value.")
   case 2...10:
     println("Large value.")
   default:
     println("Some other value.")
}
```

### Loops


arrayに対してfor/inを使用する:

```swift
for user in arrayOfUsers {
  println(user)
}
```

ディクショナリに対してfor/inを使用する:

```swift
for (key, value) in dictionary {
  println("\(key): \(value)")
}
```

1~10の数字をひとつずつindexに格納してprintlnで出力する:

```swift
for index in 1...10 {
  println("Index: \(index)")
}
```

`...`とはこの場合では1~10の数字の幅という意味で使用される。()

swiftには伝統的な`for`, `while`, and `do/while`もあります:

```swift
for var i = 0; i < 10; i++ {
    
}

var j = 0
while j < 10 {
    j++
}

var k = 0
do {
    k++
} while k < 10

```

##Nilとオプショナル型 (Nil and Optionals)
オプショナル型とは、変数の型がもつ通常の値に加えて、空の（値が無い）状態を保持できる変数です。空の状態はnilで表現します。
`nil`とは値が空の場合代わりに代入されるものです。オプショナル型で宣言された変数にアクセスするためにはアンラップしないといけません。

宣言するときは型のあとに`?`をつけます。
アンラップするときは`!`をつけます。
Declare an optional with `?`. Unwrap it with `!`.

```swift
let optionalValue : Int? = 1
if optionalValue != nil {
  let intValue = optionalValue!
}
```

`nil`はbooleanではありません。
. You must check `optionalValue != nil`. However, there's shorthand:

```swift
var optionalValue: Int? = 1
if let optionalValue = optionalValue {
  println("The int was \(optionalValue)")
} else {
  println("The int was not there.")
}
```

And a shorthand to the shorthand called a `Nil Coalescing Operator`:

```swift
var optionalValue: String?
var stringValue = optionalValue ?? ""
```

## Functions

```swift
func functionName(){
    println(“Hello World”)
}

functionName() // "Hello World"
```

With parameters:

```swift
func functionName(variableName: String){
    println(“Hello \(variableName)”)
}

functionName("Ben") // "Hello Ben"
```

With return values:

```swift
func greetingGenerator(name: String) -> String {
  return "Hello \(name)"
}

let greeting = greetingGenerator("World")
println(greeting) // "Hello World"
```

With default Values:

```swift
func functionName(name: String = "Somebody"){
    println("Hello \(name)!")
}
functionName() // "Hello Somebody"
```

For clarity, use keyword parameters:

```swift
func performGreeting(greeting:String, withName name: String){
    println("\(greeting) \(name).")
}
performGreeting("Hello", withName:"Ben")
```

To use the same keyword name as the variable name:

```swift
func performGreeting(greeting:String, #name: String){
    println("\(greeting) \(name).")
}

performGreeting("Hello", name:"Ben")
```

### Closures

Functions are just named closures.

```swift
var greetingClosure: (String, String) -> (String) = {
    (greeting, name) in
    return "\(greeting) \(name)."
}

greetingClosure("Hello", "Ben")

```

## Classes

```swift
class Animal {

}
var myAnimal = Animal()
```

### Subclassing

```swift
class Dog: Animal {
    
}

```

### Methods

```swift
class Dog: Animal {
  func bark() -> String {
    return "Woof"
  }
}

let myDog = Dog()
myDog.bark()
```

You must use `override` to override a method.

```swift
class Animal {
  func happiness() -> String {
    return "This animal does not get happy."
  }
}

class Dog: Animal {
  override func happiness() -> String {
    return "Wag tail"
  }
}
```

To call the super method, use `super.nameOfMethod()`

### Properties

There is no difference between an ivar and property.

```swift
class Dog: Animal {
    var cute = false
    func bark() -> String {
        if cute {
            return "Woof"
        } else {
            return "Growl"
        }
    }
}

var myDog = Dog()
myDog.bark()       // "Growl"
myDog.cute = true
myDog.bark()       // "Woof"
```

To add behavior normally contained in a getter or setter, use property observers:

```swift
class Dog: Animal {
  var cute = true
  var grownUp:Bool = false {
    willSet {
      println("Puppy is growing up")
    }
    didSet(oldValueForGrownUp) {
      if (grownUp){
        cute = false
      } else {
        cute = true
      }
    }
  }
}
var myDog = Dog()
myDog.cute            // True
myDog.grownUp = true
myDog.cute            // False
```

`newValue` and `oldValue` are variables available within property observers.

For properties without ivars, use computed getters and setters.

```swift
class Dog: Animal {
  var cute = false
  var adorable: Bool {
    get {
        return cute
    }
    set(newAdorable) {
        cute = newAdorable
    }
  } 
}

var myDog = Dog()
myDog.cute = true
myDog.adorable    // true
```

If the instance is declared with `let`, the object's properties are still mutable. The constant just can't point to another object.

```swift
let myDog = Dog()
myDog.cute = true // Valid
myDog = Dog()     // Invalid
```

### Protocols

```swift
protocol Domesticated {
    var name: String? { get set }
    func respondToName() -> ()
}

class Dog: Animal, Domesticated {
    var name: String?
    func respondToName() {
        println("Wag tail")
    }
}
```

### Initializers and Deinitializers

The initializer must make sure every stored property has a value before any methods are called, including `super.init()`

```swift
class Dog: Animal {
  var cute: Bool
  override init() {
    cute = true
    super.init()
  }
}
```

This is equivalent to the default initializer for:

```swift
class Dog: Animal {
  var cute = true
}
```

By overriding `init()`, you lose the default assignment behavior for all properties.

To perform cleanup code before an object is destroyed:

```swift
class Dog: Animal {
    deinit {
       println("Cleaned up")
    }
}
```

## Structs

Swift structs are like C structs, but much more powerful, resembling classes. These advanced features are covered in [[Intermediate Swift|Swift Intermediate]].

```swift
struct User {
    var name: String
    var occupation: String
}
```

By default, structs come with a member initializer.

```swift
let ben = User(name: "Ben Sandofsky", occupation:"Engineer")
```

As with Objective-C, structs are passed by value, classes are passed by reference.

Unlike a class, when a struct is declared with `let`, all of its properties are immutable.

## Enum

Like structs, Swift enums are more powerful than their C equivalents. See [[Intermediate Swift|Swift Intermediate]].

```swift
enum Color: Int {
  case Red = 1, Orange, Yellow, Green, Blue, Indigo, Violet
}
let orangeValue = Color.Orange
```

To access the underlying value, use `toRaw()`:

```swift
println("Orange raw value: \(orangeValue.toRaw()).")
```

Enums may use other underlying values:

```swift
enum ControlCharacters: Character {
  case Tab = "\t"
  case Linefeed = "\n"
  case CarriageReturn = "\r"
}
```

They can have no raw value:

```swift
enum Season {
  case Spring, Summer, Fall, Winter
}
```

If the enum type can be inferred, you can omit it.

```swift
let label = UILabel
label.textAlignment = .Right
```

## Extensions

You may extend classes, structs, and enums, without touching the original source code. It is similar to a category in Objective-C, or monkey patching in Ruby.

```swift
extension String {
    func tweetable() -> Bool {
        return countElements(self) <= 140
    }
}
```
