`defer` 可以在現在的 scope 被結束時，不管是 throw 或是 return 後，執行一段 block

```swift
func processSale(buyer: String?) throws {
    delegate?.didBeginReadingSale()
    defer { delegate?.didEndReadingSale() }
    
    guard let b = buyer else {
        throw DataError.MissingBuyer
    }

    return Sale(buyer)
}
```
