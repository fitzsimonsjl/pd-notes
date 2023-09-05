#Swift #100DOSUI

## Variables

Variables:
```swift
var name = "Jack"
```

Constants:
```swift
let name = "Jack"
```

## Strings

Strings:
```swift
	let filename = "copenhagen.jpg"
```

Reading length of string:
```swift
print(actor.count)
```

Uppercasing string:
```swift
print(result.uppercased())
```

Checking for a prefix:
```swift
print(movie.hasPrefix("Beautiful"))
```

Checking for a suffix:
```swift
print(filename.hasSuffix(".jpg"))
```

Important to know that strings are case sensitive - useful to know when filtering by prefix or suffix.

Multi-line strings:
```swift
var poem = """
First line of poem
This is the second line of the poem
And finally here's the third...
"""
```

## Integers

Whole numbers (Integers):
```swift
let score = 10
let massiveScore = 10000000 // Can also use _ as separator e.g. 10_000_000
```

Operators:
```swift
let lowerScore = score - 2
let higherScore = score + 10
let doubledscore = score * 2
let squaredScore = score * score
let halvedScore = score / 2
print(score)
```

Compound assignment operators:
```swift
counter *= 2
print(counter)

counter -=10
print(counter)

counter /= 2
print(counter)
```

Finding if an integer is a multiple of another:
```swift
let number = 120
print(number.isMultiple(of: 3))
```

Floats: 
```swift
let a = 2.4
```

You can't mix data types (floats - or Doubles) are treated as a separate data type by Swift. The only way to do so is to force Swift to mix them like so:

```Swift
// The below block will cause an error:
let a = 1
let b = 2
let c = a + b

// Tell Swift to treat Double in b as an Int:
let c = a + Int(b)

// Tell Swift to treat Int inside a as a Double:
let c = Double(a) + b
```

Swift decides if something is a Double or an Integer based on the number provided - if there's a decimal, it's a Double.

Because of type safety, we cannot change the data type of a variable like so:
```swift 
var name = "Idris Elba"
name = 24
```

Older APIs use a slightly different way of storing decimal numbers called `CGFloat` however, Swift will allow a Double wherever a CGFloat is expected so they can be safely ignored.

## Booleans