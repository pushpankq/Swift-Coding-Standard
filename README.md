
# Swift Coding Standard

## Source File Basic
### File Names
All Swift source files end with the extension  `.swift`.
A file that extends an existing type with protocol conformance is named with a combination of the type name and the protocol name, joined with a plus (`+`) sign. For more complex situations, exercise your best judgment.

Code structure and organization is a matter of pride for developers. Clear and consistent code signifies clear and consistent thought. Even though the compiler lacks a discerning palate when it comes to naming, whitespace, or documentation, it makes all the difference for human collaborators.

For example,

-   A file containing a single type  `MyType`  is named  `MyType.swift`.
-   A file containing a single extension to a type  `MyType`  that adds conformance to a protocol  `MyProtocol`  is named  `MyType+MyProtocol.swift`.
-   A file containing multiple extensions to a type  `MyType`  that add conformances, nested types, or other functionality to a type can be named more generally, as long as it is prefixed with  `MyType+`; for example,  `MyType+Additions.swift`.

### File Encoding

Source files are encoded in UTF-8.

## Apple default comment style 

Follow apple default comment style 

```swift
/// Returns the magnitude of a vector in three dimensions
/// from the given components.
///
/// - Parameters:
///     - x: The *x* component of the vector.
///     - y: The *y* component of the vector.
///     - z: The *z* component of the vector.
func magnitude3D(x: Double, y: Double, z: Double) -> Double {
    return sqrt(pow(x, 2) + pow(y, 2) + pow(z, 2))
}
```

Always leave a space after //.

Always leave comments on their own line.

### Code blocks

Demonstrate the proper usage or implementation details of a function by embedding code blocks. Inset code blocks by at least four spaces:

```swift
/**
    The area of the `Shape` instance.

    Computation depends on the shape of the instance.
    For a triangle, `area` is equivalent to:

        let height = triangle.calculateHeight()
        let area = triangle.base * height / 2
*/
var area: CGFloat { get }

```
## Naming

Descriptive and consistent naming makes software easier to read and understand. Use the Swift naming conventions described in the [API Design Guidelines](https://swift.org/documentation/api-design-guidelines/). Some key takeaways include:

- Use camelCase (initial lowercase letter) for function, method, property, constant, variable, argument names, enum cases, etc
- using uppercase for types (and protocols), lowercase for everything else
- including all needed words while omitting needless words
- using names based on roles, not types
- using terms that don't surprise experts or confuse beginners
- generally avoiding abbreviations
- use PascalCase for type names (e.g. struct, enum, class, typedef, associatedtype, etc.).
- preferring methods and properties to free functions
- casing acronyms and initialisms uniformly up or down
- giving the same base name to methods that share the same meaning
- avoiding overloads on return type
- choosing good parameter names that serve as documentation
- preferring to name the first parameter instead of including its name in the method name, except as mentioned under Delegates
- labeling closure and tuple parameters
- taking advantage of default parameters

**Preferred**:
```swift
class HomeViewController: UIViewController {
  // class stuff here
}
```
**Not Preferred**:
```swift
class Home_View_Controller: UIViewController {
  // class stuff here
}
```

-   Names should be descriptive and unambiguous.

**Preferred**:
```swift
class RoundAnimatingButton: UIButton { /* ... */ }
```

**Not Preferred**:
```swift
class CustomButton: UIButton { /* ... */ }
```

-   Do not abbreviate, use shortened names, or single letter names.

**Preferred**:
```swift
class RoundAnimatingButton: UIButton {
    let animationDuration: NSTimeInterval

    func startAnimating() {
        let firstSubview = subviews.first
    }
}
```

**Not Preferred**:
```swift
class RoundAnimating: UIButton {
    let aniDur: NSTimeInterval

    func srtAnmating() {
        let v = subviews.first
    }
}
```

### Protocol Conformance

In particular, when adding protocol conformance to a model, prefer adding a separate extension for the protocol methods. This keeps the related methods grouped together with the protocol and can simplify instructions to add a protocol to a class with its associated methods.

**Preferred**:
```swift
class MyViewController: UIViewController {
  // class stuff here
}

// MARK: - UITableViewDataSource
extension MyViewController: UITableViewDataSource {
  // table view data source methods
}

// MARK: - UIScrollViewDelegate
extension MyViewController: UIScrollViewDelegate {
  // scroll view delegate methods
}
```

**Not Preferred**:
```swift
class MyViewController: UIViewController, UITableViewDataSource, UIScrollViewDelegate {
  // all methods
}
```

### Code grouping 
A good manner of coding is to group a code into the logical parts. Use // MARK
And break functionality into parts with the help of extension.

```swift
// MARK: - ViewController Life Cycle 
extension HomeViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        checkPermission()
     }
 
 override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
        loadAsset(with: self.asset)
    }
}
    
// MARK: - IBActions
extension HomeViewController {
    @IBAction func actionCancel(_ sender: Any) {
        self.dismiss(animated: true)
    }
}
```


### Minimal Imports

Import only the modules a source file requires. For example, don't import `UIKit` when importing `Foundation` will suffice. Likewise, don't import `Foundation` if you must import `UIKit`.

**Preferred**:

```swift
import UIKit
var view: UIView
var deviceModels: [String]
```

**Preferred**:

```swift
import Foundation
var deviceModels: [String]
```

**Not Preferred**:
```swift
import UIKit
import Foundation
var view: UIView
var deviceModels: [String]
```

**Not Preferred**:

```swift
import UIKit
var deviceModels: [String]
```

### Brackets

Do not place opening braces on new lines

**Preferred**:
```swift
if user.isHappy {
  // Do something
} else {
  // Do something else
}
```

**Not Preferred**:
```swift
if user.isHappy
{
  // Do something
}
else {
  // Do something else
}
```
### Semicolons

Semicolon is not required in SWIFT. 

**Preferred**:
```swift
let anyString = "This is random string"
```

**Not Preferred**:
```swift
let anyString = "This is random string";
```
### Spacing

Colons always have no space on the left and one space on the right. Exceptions are the ternary operator ? :, empty dictionary [:] and #selector syntax addTarget(_:action:).

**Preferred**:
```swift
class TestDatabase: Database {
  var data: [String: CGFloat] = ["A": 1.2, "B": 3.2]
}
```

**Not Preferred**:
```swift
class TestDatabase : Database {
  var data :[String:CGFloat] = ["A" : 1.2, "B":3.2]
}
```
 In general, there should be a space following a comma.
 ```swift
let myArray = [1, 2, 3, 4, 5]
```
### Horizontal Whitespace

1. Separating any reserved word starting a conditional or switch statement (such as if, guard, while, or switch) from the expression that follows it if that expression starts with an open parenthesis (()

**Preferred**:
```swift
if (x == 0 && y == 0) || z == 0 {
  // ...
}
```

**Not Preferred**:
```swift
if(x == 0 && y == 0) || z == 0 {
  // ...
}
```
2. Before any closing curly brace (}) that follows code on the same line, before any open curly brace ({), and after any open curly brace ({) that is followed by code on the same line.

**Preferred**:
```swift
let nonNegativeCubes = numbers.map { $0 * $0 * $0 }.filter { $0 >= 0 }
```

**Not Preferred**:
```swift
let nonNegativeCubes = numbers.map { $0 * $0 * $0 } .filter { $0 >= 0 }
```

**Not Preferred**:
```swift
let nonNegativeCubes = numbers.map{$0 * $0 * $0}.filter{$0 >= 0}
```

3. On both sides of any binary or ternary operator, including the “operator-like” symbols described below, with exceptions noted at the end:

    a. The = sign used in assignment, initialization of variables/properties, and default arguments in functions.
**Preferred**:
```swift
            var x = 5

            func sum(_ numbers: [Int], initialValue: Int = 0) {
                // ...
            }
 ```
**Not Preferred**:

```swift
var x=5

func sum(_ numbers: [Int], initialValue: Int=0) {
  // ...
}
```
   b. The ampersand (&) in a protocol composition type.
        
**Preferred**:

```swift
func sayHappyBirthday(to person: NameProviding & AgeProviding) {
  // ...
}
```

**Not Preferred**:

```swift
func sayHappyBirthday(to person: NameProviding&AgeProviding) {
  // ...
}
```

   c. The operator symbol in a function declaring/implementing that operator.
**Preferred**:

```swift
static func == (lhs: MyType, rhs: MyType) -> Bool {
  // ...
}
```
**Not Preferred**:

```swift
static func ==(lhs: MyType, rhs: MyType) -> Bool {
  // ...
}
```

   d. The arrow (->) preceding the return type of a function.
        
**Preferred**:

```swift
func sum(_ numbers: [Int]) -> Int {
  // ...
} 
```
**Not Preferred**:
```swift
func sum(_ numbers: [Int])->Int {
  // ...
}
```
   e. #### Exception: There is no space on either side of the dot (.) used to reference value and type members.
   
**Preferred**:

```swift
let width = view.bounds.width 
```
**Not Preferred**:

```swift
let width = view . bounds . width
```

### Use of Self

For conciseness, avoid using `self` since Swift does not require it to access an object's properties or invoke its methods.

Use self only when required by the compiler (in `@escaping` closures, or in initializers to disambiguate properties from arguments). In other words, if it compiles without `self` then omit it.

### Computed Properties

For conciseness, if a computed property is read-only, omit the get clause. The get clause is required only when a set clause is provided.

**Preferred**:
```swift
var diameter: Double {
  return radius * 2
}
```

**Not Preferred**:
```swift
var diameter: Double {
  get {
    return radius * 2
  }
}
```

## Closure Expressions

Use trailing closure syntax only if there's a single closure expression parameter at the end of the argument list. Give the closure parameters descriptive names.

**Preferred**:
```swift
UIView.animate(withDuration: 1.0) {
  self.myView.alpha = 0
}

UIView.animate(withDuration: 1.0, animations: {
  self.myView.alpha = 0
}, completion: { finished in
  self.myView.removeFromSuperview()
})
```

**Not Preferred**:
```swift
UIView.animate(withDuration: 1.0, animations: {
  self.myView.alpha = 0
})

UIView.animate(withDuration: 1.0, animations: {
  self.myView.alpha = 0
}) { f in
  self.myView.removeFromSuperview()
}
```

For single-expression closures where the context is clear, use implicit returns:

```swift
attendeeList.sort { a, b in
  a > b
}
```

Chained methods using trailing closures should be clear and easy to read in context. Decisions on spacing, line breaks, and when to use named versus anonymous arguments is left to the discretion of the author. Examples:

```swift
let value = numbers.map { $0 * 2 }.filter { $0 % 3 == 0 }.index(of: 90)

let value = numbers
  .map {$0 * 2}
  .filter {$0 > 50}
  .map {$0 + 10}
```
## Types

Always use Swift's native types and expressions when available. Swift offers bridging to Objective-C so you can still use the full set of methods as needed.

**Preferred**:
```swift
let width = 120.0                                    // Double
let widthString = "\(width)"                         // String
```

**Less Preferred**:
```swift
let width = 120.0                                    // Double
let widthString = (width as NSNumber).stringValue    // String
```

**Not Preferred**:
```swift
let width: NSNumber = 120.0                          // NSNumber
let widthString: NSString = width.stringValue        // NSString
```

In drawing code, use `CGFloat` if it makes the code more succinct by avoiding too many conversions.

## Constants

Constants are defined using the let keyword and variables with the var keyword. Always use let instead of var if the value of the variable will not change.

Tip: A good technique is to define everything using let and only change it to var if the compiler complains!

**Preferred**:
```swift
enum Math {
  static let e = 2.718281828459045235360287
  static let root2 = 1.41421356237309504880168872
}

let hypotenuse = side * Math.root2

```

**Less Preferred**:
```swift
struct Math {
  static let e = 2.718281828459045235360287
  static let root2 = 1.41421356237309504880168872
}

let hypotenuse = side * Math.root2

```
**Note:** The advantage of using a case-less enumeration is that it can't accidentally be instantiated and works as a pure namespace.

**Not Preferred**:
```swift
let e = 2.718281828459045235360287  // pollutes global namespace
let root2 = 1.41421356237309504880168872

let hypotenuse = side * root2 // what is root2?
```

### Type Inference

Prefer compact code and let the compiler infer the type for constants or variables of single instances. Type inference is also appropriate for small, non-empty arrays and dictionaries. When required, specify the specific type such as `CGFloat` or `Int16`.

**Preferred**:
```swift
let message = "Click the button"
let currentBounds = computeViewBounds()
var names = ["Mic", "Sam", "Christine"]
let maximumWidth: CGFloat = 106.5
```

**Not Preferred**:
```swift
let message: String = "Click the button"
let currentBounds: CGRect = computeViewBounds()
var names = [String]()
```

#### Type Annotation for Empty Arrays and Dictionaries

For empty arrays and dictionaries, use type annotation. (For an array or dictionary assigned to a large, multi-line literal, use type annotation.)

**Preferred**:
```swift
var names: [String] = []
var lookup: [String: Int] = [:]
```

**Not Preferred**:
```swift
var names = [String]()
var lookup = [String: Int]()
```

**NOTE**: Following this guideline means picking descriptive names is even more important than before.

### Syntactic Sugar

Prefer the shortcut versions of type declarations over the full generics syntax.

**Preferred**:
```swift
var deviceModels: [String]
var employees: [Int: String]
var faxNumber: Int?
```

**Not Preferred**:
```swift
var deviceModels: Array<String>
var employees: Dictionary<Int, String>
var faxNumber: Optional<Int>
```

## Optionals

Declare variables and function return types as optional with `?` where a `nil` value is acceptable.

**Preferred**:
```swift
if
    let id = jsonObject[Constants.Id] as? Int,
    let firstName = jsonObject[Constants.firstName] as? String,
    let lastName = jsonObject[Constants.lastName] as? String,
    let initials = jsonObject[Constants.initials] as? String {
        // Flat
        let user = User(id: id, name: name, initials: initials)
        // ...
}
```

**Not Preferred**:
```swift
if let id = jsonObject[Constants.id] as? Int {
    if let firstName = jsonObject[Constants.firstName] as? String {
        if let lastName = jsonObject[Constants.lastName] as? String {
            if let initials = jsonObject[Constants.initials] as? String {
                // Deep nesting
                let user = User(id: id, firstName: name, lastName: lastName, initials: initials)
                // ...
            }
        }
    }
}
```

## Memory Management

Code (even non-production, tutorial demo code) should not create reference cycles. Analyze your object graph and prevent strong cycles with `weak` and `unowned` references. Alternatively, use value types (`struct`, `enum`) to prevent cycles altogether.

### Extending object lifetime

Extend object lifetime using the `[weak self]` and `guard let self = self else { return }` idiom. `[weak self]` is preferred to `[unowned self]` where it is not immediately obvious that `self` outlives the closure. Explicitly extending lifetime is preferred to optional chaining.

**Preferred**
```swift
resource.request().onComplete { [weak self] response in
  guard let self = self else {
    return
  }
  let model = self.updateModel(response)
  self.updateUI(model)
}
```

**Not Preferred**
```swift
// might crash if self is released before response returns
resource.request().onComplete { [unowned self] response in
  let model = self.updateModel(response)
  self.updateUI(model)
}
```

**Not Preferred**
```swift
// deallocate could happen between updating the model and updating UI
resource.request().onComplete { [weak self] response in
  let model = self?.updateModel(response)
  self?.updateUI(model)
}
```

## Multi-line String Literals

**Preferred**

```swift
let message = """
  You cannot charge the flux \
  capacitor with a 9V battery.
  You must use a super-charger \
  which costs 10 credits. You currently \
  have \(credits) credits available.
  """
  ```

**Not Preferred**

```swift
let message = """You cannot charge the flux \
  capacitor with a 9V battery.
  You must use a super-charger \
  which costs 10 credits. You currently \
  have \(credits) credits available.
  """
  ```

**Not Preferred**

```swift
let message = "You cannot charge the flux " +
  "capacitor with a 9V battery.\n" +
  "You must use a super-charger " +
  "which costs 10 credits. You currently " +
  "have \(credits) credits available."
  ```
  
  ## Initializers
  
  For clarity, initializer arguments that correspond directly to a stored property have the same name as the property. Explicit self. is used during assignment to disambiguate them.
  
  **Preferred**
```swift
  public struct Person {
  public let name: String
  public let phoneNumber: String

  // GOOD.
  public init(name: String, phoneNumber: String) {
    self.name = name
    self.phoneNumber = phoneNumber
  }
}
```

**Not Preferred**

```swift

public struct Person {
  public let name: String
  public let phoneNumber: String

  // AVOID.
  public init(name otherName: String, phoneNumber otherPhoneNumber: String) {
    name = otherName
    phoneNumber = otherPhoneNumber
  }
}
```
## Ternary operator

The Ternary operator, `?:` , should only be used when it increases clarity or code neatness. A single condition is usually all that should be evaluated. Evaluating multiple conditions is usually more understandable as an `if` statement or refactored into instance variables. In general, the best use of the ternary operator is during assignment of a variable and deciding which value to use.

**Preferred**:

```swift
let value = 5
result = value != 0 ? x : y

let isHorizontal = true
result = isHorizontal ? x : y
```

**Not Preferred**:

```swift
result = a > b ? x = c > d ? c : d : y
```

## For Loop 

**Preferred**:

```swift
 for i in 0...15 where i == 4  {
    print("its four")
 }
```

**Not Preferred**:

```swift
for i in 0...15 {
    if i == 4 {
        print("its four")
    }
 }
```
## Access Control

Full access control annotation in tutorials can distract from the main topic and is not required. Using `private` and `fileprivate` appropriately, however, adds clarity and promotes encapsulation. Prefer `private` to `fileprivate`; use `fileprivate` only when the compiler insists.

Only explicitly use `open`, `public`, and `internal` when you require a full access control specification.

Use access control as the leading property specifier. The only things that should come before access control are the `static` specifier or attributes such as `@IBAction`, `@IBOutlet` and `@discardableResult`.

**Preferred**:
```swift
private let message = "Great Scott!"

class TimeMachine {  
  private dynamic lazy var fluxCapacitor = FluxCapacitor()
}
```

**Not Preferred**:
```swift
fileprivate let message = "Great Scott!"

class TimeMachine {  
  lazy dynamic private var fluxCapacitor = FluxCapacitor()
}
```

## Function 

Don't use `(Void)` to represent the lack of an input; simply use `()`. Use `Void` instead of `()` for closure and function outputs.

**Preferred**:

```swift
func updateConstraints() -> Void {
  // magic happens here
}

typealias CompletionHandler = (result) -> Void
```

**Not Preferred**:

```swift
func updateConstraints() -> () {
  // magic happens here
}

typealias CompletionHandler = (result) -> ()
```

#### Make classes `final` by default

Classes should start as `final`, and only be changed to allow subclassing if a valid need for inheritance has been identified. Even in that case, as many definitions as possible _within_ the class should be `final` as well, following the same rules.

## High Order Function 

Prefer the composition of map, filter, reduce, etc. over iterating when transforming from one collection to another. Make sure to avoid using closures that have side effects when using these methods.

**Preferred**:
```swift
let stringOfInts = [1, 2, 3].flatMap { String($0) }
// ["1", "2", "3"]
```

**Not Preferred**:
```swift
var stringOfInts: [String] = []
for integer in [1, 2, 3] {
    stringOfInts.append(String(integer))
}
```

**Preferred**:
```swift
let evenNumbers = [4, 8, 15, 16, 23, 42].filter { $0 % 2 == 0 }
// [4, 8, 16, 42]
```

**Not Preferred**:
```swift
var evenNumbers: [Int] = []
for integer in [4, 8, 15, 16, 23, 42] {
    if integer % 2 == 0 {
        evenNumbers.append(integer)
    }
}
```

## References

* [Raywenderlich swift style guide](https://github.com/raywenderlich/swift-style-guide)
* [Google swift style guide](https://google.github.io/swift/)
* [The Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines/)
* [The Swift Programming Language](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/index.html)
* [Using Swift with Cocoa and Objective-C](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/BuildingCocoaApps/index.html)
* [Swift Standard Library Reference](https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/SwiftStandardLibraryReference/index.html)

