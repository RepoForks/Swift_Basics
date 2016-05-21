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

