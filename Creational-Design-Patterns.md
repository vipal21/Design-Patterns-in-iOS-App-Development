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

Native Example: UIButton

```
import UIKit

// Factory method for creating UIButton
let button = UIButton(type: .system)

// Usage:
button.setTitle("Tap me", for: .normal)
button.frame = CGRect(x: 100, y: 100, width: 200, height: 40)
view.addSubview(button)

```
Explanation: In this code, UIButton(type:) is a factory method provided by UIKit. It creates a UIButton with a specific style (e.g., .system, .roundedRect, etc.).
