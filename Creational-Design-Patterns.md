# Design-Patterns-in-iOS-App-Development

Certainly! Creational design patterns are a set of guidelines or templates for creating objects in software. They help you solve the problem of "how to create objects" in a way that is efficient, flexible, and easy to manage.
Imagine you are building a house, and you need to create different types of rooms: a bedroom, a living room, and a kitchen. Creational design patterns provide you with different methods or blueprints for creating these rooms.

Here are some simple explanations of common creational design patterns:

1) Singleton: It's like ensuring there is only one key to a special room in your house. No matter how many times you ask for the key, you always get the same one.
2) Factory Method: Think of it as a factory that produces different types of cars. You tell the factory what kind of car you want, and it gives you that specific type of car.
3) Abstract Factory: Imagine a furniture factory that produces both chairs and tables. You can choose to get either a modern chair and modern table or a classic chair and classic table. The factory lets you create sets of related objects.
4) Builder: This is like a step-by-step process to build a complex object, like building a custom computer by choosing the processor, memory, and other components one by one.
5) Prototype: It's like making a photocopy of an existing object. You create a new object by copying an existing one.

In summary, creational design patterns provide ways to create objects in software by defining rules and structures for doing so. These patterns help you manage object creation efficiently and consistently throughout your code.

# Singleton
It's like ensuring there is only one key to a special room in your house. No matter how many times you ask for the key, you always get the same one.
```
class Singleton {
    static let shared = Singleton() // Create a single instance accessible throughout the app
    
    private init() {
        // Private constructor to prevent external instantiation
    }
    
    func doSomething() {
        print("Singleton is doing something.")
    }
}

// Usage:
let singleton = Singleton.shared
singleton.doSomething()

```
In this example, Singleton is a class that follows the Singleton pattern. It ensures that only one instance of Singleton can be created, and that instance is accessed via the shared property.

Native Example: UIApplication and UserDefaults.

```
import UIKit

// Apple's UIApplication class is a Singleton
let appDelegate = UIApplication.shared.delegate as! AppDelegate

// Usage:
let statusBarFrame = appDelegate.statusBarFrame
```
Explanation: UIApplication is a singleton because there should only be one instance of the application object representing your app. Similarly, UserDefaults provides a single interface to access user preferences and is designed as a singleton to maintain consistency throughout the app.

# Factory Method
Defines an interface for creating an object but allows subclasses to alter the type of objects that will be created.
```
import UIKit

// Factory method to create different views
func createView(type: String) -> UIView {
    switch type {
    case "Label":
        return UILabel()
    case "Button":
        return UIButton()
    default:
        return UIView()
    }
}

// Usage:
let labelView = createView(type: "Label")
let buttonView = createView(type: "Button")
```
In this example, the createView function acts as a factory method. It takes a parameter type and returns a different type of UIView based on the input.

Native Example: UIView

```
import UIKit

// Factory method for creating UIButton
let button = UIButton(type: .system)

// Usage:
button.setTitle("Tap me", for: .normal)
button.frame = CGRect(x: 100, y: 100, width: 200, height: 40)
view.addSubview(button)

```
Explanation: UIView is a factory for creating different types of views like labels, buttons, and image views. You call methods like UILabel() or UIButton() to create instances of specific view types.

# Abstract Factory: 
Provides an interface for creating families of related or dependent objects without specifying their concrete classes.
```
import UIKit

// Abstract factory for creating fonts
protocol FontFactory {
    func createFont() -> UIFont
}

// Concrete factory for system fonts
class SystemFontFactory: FontFactory {
    func createFont() -> UIFont {
        return UIFont.systemFont(ofSize: 14.0)
    }
}

// Concrete factory for custom fonts
class CustomFontFactory: FontFactory {
    func createFont() -> UIFont {
        return UIFont(name: "CustomFont", size: 16.0) ?? UIFont.systemFont(ofSize: 16.0)
    }
}

// Usage:
let systemFontFactory = SystemFontFactory()
let customFontFactory = CustomFontFactory()

let systemFont = systemFontFactory.createFont()
let customFont = customFontFactory.createFont()

```
In this example, we define an abstract factory FontFactory with a method createFont(). Two concrete factories (SystemFontFactory and CustomFontFactory) implement this protocol to create different types of fonts.

Native Example: UIFont and UIColor

```
import UIKit

// Abstract factory for creating fonts
let systemFont = UIFont.systemFont(ofSize: 16.0)
let customFont = UIFont(name: "CustomFont", size: 16.0) ?? UIFont.systemFont(ofSize: 16.0)

// Abstract factory for creating colors
let redColor = UIColor.red
let customColor = UIColor(displayP3Red: 0.2, green: 0.4, blue: 0.6, alpha: 1.0)


```
Explanation: In this code, UIFont.systemFont(ofSize:) and UIFont(name:size:) are abstract factories for creating fonts with different styles. Similarly, UIColor provides various factory methods for creating colors.

# Builder
This is like a step-by-step process to build a complex object, like building a custom computer by choosing the processor, memory, and other components one by one.
```
import Foundation

class RequestBuilder {
    private var url: URL?
    private var method: String = "GET"
    private var headers: [String: String] = [:]
    private var body: Data?

    func setURL(_ url: URL) -> RequestBuilder {
        self.url = url
        return self
    }

    func setMethod(_ method: String) -> RequestBuilder {
        self.method = method
        return self
    }

    func setHeaders(_ headers: [String: String]) -> RequestBuilder {
        self.headers = headers
        return self
    }

    func setBody(_ body: Data) -> RequestBuilder {
        self.body = body
        return self
    }

    func build() -> URLRequest {
        guard let url = self.url else {
            fatalError("URL is required to build the request.")
        }
        var request = URLRequest(url: url)
        request.httpMethod = method
        request.allHTTPHeaderFields = headers
        request.httpBody = body
        return request
    }
}

// Usage:
let url = URL(string: "https://example.com")!
let request = RequestBuilder()
    .setURL(url)
    .setMethod("POST")
    .setHeaders(["Content-Type": "application/json"])
    .setBody(Data())
    .build()

```
In this example, RequestBuilder follows the Builder pattern to construct a URLRequest. You can chain methods to set different attributes of the request, and then call build() to create the final request.

Native Example: UIFont and UIColor

```
import Foundation

// Builder pattern for creating a URLRequest
var request = URLRequest(url: URL(string: "https://example.com")!)
request.httpMethod = "POST"
request.allHTTPHeaderFields = ["Content-Type": "application/json"]
request.httpBody = Data()
```
Explanation: In this code, we are using the builder pattern to create a URLRequest. We initialize a basic request and then set its attributes step by step.
