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

