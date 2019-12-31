
# Swift Coding Standard

## Source File Basics
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

```
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

### Code blocks

Demonstrate the proper usage or implementation details of a function by embedding code blocks. Inset code blocks by at least four spaces:

```
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

- using camel case (not snake case)
- using uppercase for types (and protocols), lowercase for everything else
- including all needed words while omitting needless words
- using names based on roles, not types
- striving for fluent usage
- beginning factory methods with `make`
- using terms that don't surprise experts or confuse beginners
- generally avoiding abbreviations
- using precedent for names
- preferring methods and properties to free functions
- casing acronyms and initialisms uniformly up or down
- giving the same base name to methods that share the same meaning
- avoiding overloads on return type
- choosing good parameter names that serve as documentation
- preferring to name the first parameter instead of including its name in the method name, except as mentioned under Delegates
- labeling closure and tuple parameters
- taking advantage of default parameters

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

### Minimal Imports

Import only the modules a source file requires. For example, don't import `UIKit` when importing `Foundation` will suffice. Likewise, don't import `Foundation` if you must import `UIKit`.

**Preferred**:
```
import UIKit
var view: UIView
var deviceModels: [String]
```

**Preferred**:
```
import Foundation
var deviceModels: [String]
```

**Not Preferred**:
```
import UIKit
import Foundation
var view: UIView
var deviceModels: [String]
```

**Not Preferred**:
```
import UIKit
var deviceModels: [String]
```

### Brackets

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

### Use of Self

For conciseness, avoid using `self` since Swift does not require it to access an object's properties or invoke its methods.

Use self only when required by the compiler (in `@escaping` closures, or in initializers to disambiguate properties from arguments). In other words, if it compiles without `self` then omit it.
