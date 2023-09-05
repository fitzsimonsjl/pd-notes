## Booleans

Simply return true or false (like the examples for `hasSuffix`or `isMultiple`in Day 1)

When creating a boolean, an initial value of true or false must be assigned - you can also assign a boolean's initial value from other code so long as it's true or false.

It's possible to flip a boolean value using `.toggle()`:
```swift
var gameOver = false
print(gameOver)

gameOver.toggle()
print(gameOver)
```

## String Interpolation

The easiest way is to use `+` to join them together:
```swift
let firstHalf = "This is the first half"
let secondHalf = "of the entire example sentence"

let exampleString = firstHalf + secondHalf
```

Best to avoid - becomes awkward, not very efficient. Instead we can use the equivalent of an fstring in Python:
```swift 
let name = "Jack"
let age = 30
let message = "\(name) is \(age) and is getting on a bit..."
```

It's also possible to do calculations inside string interpolation:
```swift
print("8 x 12 is \(8 * 12)")
```

