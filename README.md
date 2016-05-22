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
swift2.0以降では`println`は廃止されてしまい、`print`を使うようになりました。そのまま`print`を使用すると\nが行末に表示されてしまいますが、`改行なしの場合は、terminatorとして空文字（””）を渡します。`以後`print`をこのノートで扱う際は\nがprintされるのは気にせず書きます。

```swift
let myColors = ("Green", "Blue", "Indigo", "Violet")
print(myColors.2) // "Indigo"
print(myColors.2, terminator:"")
```
以下のような使い方をすると便利ですね。

```swift
let myResponse: (code: Int, message: String) = (200, "OK")
print(myResponse.message)
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
  print("The value was 1.")
}
```

### Switch
switch文を使うと、値に応じた処理内容を記述することができます。値のパターンが多い場合、if文を使うより見通しよく書けます。C言語やJavaのswitch文と似ていますが、Swiftのswitch文はより柔軟な比較判定が可能です。

```swift
switch someValue {
   case 1:
     print("Hit single value.")
   case 2...10:
     print("Large value.")
   default:
     print("Some other value.")
}
```

### Loops


arrayに対してfor/inを使用する:

```swift
for user in arrayOfUsers {
  print(user)
}
```

ディクショナリに対してfor/inを使用する:

```swift
for (key, value) in dictionary {
  print("\(key): \(value)")
}
```

1~10の数字をひとつずつindexに格納してprintで出力する:

```swift
for index in 1...10 {
  print("Index: \(index)")
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
一度`optionalValue != nil`をチェックしてみたらわかります。
. You must check `optionalValue != nil`. However, there's shorthand:

```swift
var optionalValue: Int? = 1
//この行がポイント！今回上の行でoptionalValueには値が代入されているので
//let optionalValueにはnilではなく1が代入されるのでifが返す値は真(true)
if let optionalValue = optionalValue { 
  print("The int was \(optionalValue)")
} else {
  print("The int was not there.")
}
```

アンラップをショートカットする書き方もあります。Swiftでは??（はてな二つ）を使って値がnilのときに代入する値を指定することができます。

```swift
let fuga = hoge ?? "hage"
```
上の例では、hogeがnilでないときはhogeの中身をfugaに代入し、hogeがnilのときは文字列"hage"をfugaに代入しています。

##関数 (Functions)
関数とは命令のかたまりだとおもってください。swiftでは以下のように関数を書くのが基本です。
```swift
func functionName(){
    print(“Hello World”)
}

functionName() // "Hello World"
```

引数(parameters)をとる場合:

```swift
func functionName(variableName: String){
    print(“Hello \(variableName)”)
}

functionName("Hanako") // "Hello Hanako"
```

返り値(return values)を返す場合:

```swift
func greetingGenerator(name: String) -> String {
  return "Hello \(name)"
}

let greeting = greetingGenerator("World")
print(greeting) // "Hello World"
```

引数に規定値(default value)を与える場合:

```swift
func functionName(name: String = "Somebody"){
    print("Hello \(name)!")
}
functionName() // "Hello Somebody"
```

外部引数名(keyword parameters):
関数の各引数には、引数名（ローカル名）の他に、分かりやすいラベル（外部名）をつけて、呼び出し時に使うことができます。ラベルをつける事で関数自体がより説明的になり機能や意味が伝わりやすくなります。

```swift
func performGreeting(greeting:String, withName name: String){
    print("\(greeting) \(name).")
}
performGreeting("Hello", withName:"Ben")
```

キーワード`name`をそのまま変数nameとして利用する場合:

```swift
func performGreeting(greeting:String, name: String){
    print("\(greeting) \(name).")
}

performGreeting("Hello", name:"Ben")
```

###　クロージャ (Closures)

関数を呼び出す側のスコープで定義された変数を、内側の関数で参照したり変更することができます。これはクロージャと呼ばれるものです。

```swift
func makeIncrementer(initValue: Int) -> () -> Int {
    var v = initValue
    func incrementer() -> Int {
        return v += 1
    }
    
    return incrementer
}

let inc = makeIncrementer(10)
inc()   // 11
inc()   // 12
inc()   // 13
```

## クラス(Classes)

```swift
class Animal {

}
var myAnimal = Animal()
```

### サブクラス(Subclassing)

```swift
class Dog: Animal {
    
}

```

### メソッド(Methods)

```swift
class Dog: Animal {
  func bark() -> String {
    return "Woof"
  }
}

let myDog = Dog()
myDog.bark()
```

スーバークラスで既に定義されているメソッドと同じシグニチャ（同じ名前、同じ引数、同じ戻り値）のメソッドを定義する場合は、overrideを指定する必要があります。これは誤ってスーバークラスのメソッドを上書きしてしまうミスを防ぐためです。overrideを指定したメソッドと同じメソッドがスーバークラス（継承ツリーのどこか）に定義されていない場合もエラーになります。

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



### プロパティ(Properties)

Swiftでは、クラス、構造体、列挙型にプロパティを持たせることができます。プロパティとはこれらの型に関連づけられた属性のことです。



```swift
class Person {
    let name: String    // 名前
    var age: Int        // 年齢

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
}

var p = Person(name: "山田太郎", age: 25)
p.age = 30
p.name = "鈴木花子" // エラー
```

保持型プロパティの宣言の前にlazyというキーワードをつけると、遅延評価させることができます。
例えば、lazy var hoge: Hoge と宣言すると、hogeというプロパティに実際にアクセスがあるまで、hogeは生成されません。これは、生成にコストがかかるようなインスタンスで、実際にそれが使用されるとは限らないような場合に指定すると、パフォーマンスの向上が期待できます。

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


###プロトコル(Protocols)
Javaでいうインターフェースみたいなものです。クラスの挙動を決めた設計図みたいなものです。

```swift
protocol SomeProtocol {
    // インターフェースの定義
    func someMethod()
    :
}


struct SomeStructure: SomeProtocol {
    func someMethod()
    :
}
```

### イニシャライザとデイニシャライザ(Initializers and Deinitializers)

イニシャライザはinitという名の特別なメソッドで、構造体とクラスで初期化のために使用します。

```swift
/* パーソン */
struct Person {
    var name: String    // 名前
    var age: Int        // 年齢
    // イニシャライザ
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
}
let person = Person(name:"タロウ", age: 18)
```



デイニシャライザはクラスのインスタンスが破棄される時に自動的に呼ばれる特殊なメソッドです。構造体にデイニシャライザはありません。
メモリに確保されたインスタンスやプロパティはARC（Automatic reference counting）によって自動的に破棄されるので通常はデイニシャライザを記述する必要はありませんが、例えばファイルを扱うクラスで、開いたファイルをインスタンスの破棄時に確実に閉じるためにデイニシャライザを利用することができます。
デイニシャライザは次のように、deinitという名のメソッドです。deinitの後の()（かっこ）は不要です。

```swift
deinit {
    // 後始末
}
```

## 構造体(Structs)

カプセル化を実現する方法としてSwiftには、クラスの他に構造体（struct）が用意されています。

 - 構造体では継承は利用できません。
 - 構造体にデイニシャライザは定義できません。
 - クラスのインスタンスを別の変数に代入すると参照が渡されます。インスタンスの参照数は参照カウントで管理されます。対して構造体を別の変数に代入すると新たなコピーが生成されます。構造体の参照先は常に１つなので参照カウントは使用されません。

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

## Enum

列挙型は、関連する値を型としてまとめたものです

```swift
enum Color: Int {
  case Red = 1, Orange, Yellow, Green, Blue, Indigo, Violet
}
let orangeValue = Color.Orange
```


## エクステンション(Extensions)
直接ソースコードをいじることなくクラス、構造体、列挙型を拡張することができます。


```swift
extension String {
    func tweetable() -> Bool {
        return countElements(self) <= 140
    }
}
```
