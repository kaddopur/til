用 `try!` 來表示一段 expression 不可能會發生 error
如果真的 error 了，它會直接讓 app crash

```swift
func foo() {
    try! someConditionCheck()
    doTask()
}
```

等同於

```swift
func foo() {
    do {
        try someConditionCheck()
        doTask()
    } catct {
        fatalError("It should not go here!")
    }
}
```
