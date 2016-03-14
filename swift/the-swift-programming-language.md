# The Swift Programming Language (Swift 2.2 Prerelease)

## Functions

終於知道為什麼要這樣子寫 function name 了(連續兩個 sender)

```swift
func prepareForSegue(_ segue: UIStoryboardSegue, sender sender: AnyObject?)
```

- external parameter name
- local parameter name

```swift
func sayHello(to person: String, and anotherPerson: String) -> String {
    return "Hello \(person) and \(anotherPerson)!"
}

sayHello(to: "Bill", and: "Ted")
```


`inout` 關鍵字可以讓 func 可以修改傳進來的 parameters
```swift
var foo = 1

func increment(inout number: Int) {
    number += 1
}

increment(&foo)
// foo = 2
```

## Closures

sort 可以這樣子寫，都等義
```swift
var foo = [2, 5, 3, 1]

func backwards(lhs: Int, rhs: Int) -> Bool {
    return lhs > rhs
}

foo.sort({(lhs: Int, rhs: Int) -> Bool in
    return lhs > rhs
})

foo.sort({lhs, rhs in return lhs > rhs })

foo.sort({lhs, rhs in lhs > rhs })

foo.sort({$0 > $1})

foo.sort(>)
```

## Enumerations

### associated values

```swift
enum Barcode {
    case UPCA(Int, Int, Int, Int)
    case QRCode(String)
}
```

### raw values
必須為同一種型別，值相異

```swift
enum ASCII: Character {
    case Tab = "\t"
}
```


## Classes and Structures
### classes
- Reference Type

### structures
- Value Type!!!
- String, Array, Dictionary 也是 Value Type!!!
- assign 或是當做參數傳入 function 時，會假性 copy 一份 (Swift 會最佳化 copy 程序)

## Properties

- Stored properties vs Computed properties

```swift
struct Foo {
    var storedProperty = 2.0
    var computedProperty: Int {
        get {
            return Int(storedProperty * 10)
        }
        
        set {
            storedProperty = Double(newValue) / 10.0
        }
    }
    
    var shortComputedProperty: Int {
        return Int(storedProperty * 10)
    }
}
```

- Property Observers
```swift
struct Bar {
    var step = 0 {
        willSet {
            print("Step will be set to \(newValue)")
        }
        
        didSet {
            if step > 10 {
                step = 10
            }
        }
    }
}
```

- `static` & `class` keyword for Type properties
```swift
class SomeClass {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 27
    }
    class var overrideableComputedTypePorperty: Int {
        return 107
    }
}
```

## Subscripts
可以對 class, struct 與 enumerion 定義 subscript，傳入的參數可以是任意 type，參數的個數也可以傳入多個，可以看做是一個方便用方括號取值的函式

```swift
struct TimesTable {
    let multiplier: Int
    subscript(key: String) -> String {
        var output = ""
        for _ in 0..<multiplier {
            output += key
        }
        return output
    }
}

let threeTimesTable = TimesTable(multiplier: 4)
threeTimesTable["foo"]
threeTimesTable["bar"]
```
 
