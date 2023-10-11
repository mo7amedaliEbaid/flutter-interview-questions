# Dart-Flutter-interview-questions

<p float="left">
   <img src="https://github.com/mo7amedaliEbaid/dart-flutter-interview-questions/blob/bc8d06480cef61c36a481e1915a0ff4880213b9a/assets/feynman1.jpg" width="770" />
</p>

## 0-Flutter architectural overview.

- Flutter is a cross-platform UI toolkit that is designed to allow code reuse across operating systems such as iOS and Android, while also allowing applications to interface directly with underlying platform services. The goal is to enable developers to deliver high-performance apps that feel natural on different platforms, embracing differences where they exist while sharing as much code as possible.

- During development, Flutter apps run in a VM that offers stateful hot reload of changes without needing a full recompile. For release, Flutter apps are compiled directly to machine code, whether Intel x64 or ARM instructions, or to JavaScript if targeting the web. The framework is open source, with a permissive BSD license, and has a thriving ecosystem of third-party packages that supplement the core library functionality.


### Architectural layers.
<p float="left">
   <img src="https://github.com/mo7amedaliEbaid/dart-flutter-interview-questions/blob/b3f2edbccd35b594ea589729248c3d4b322938ca/assets/flutt.png" width="770" />
</p>

- Flutter is designed as an extensible, layered system. It exists as a series of independent libraries that each depend on the underlying layer. No layer has privileged access to the layer below, and every part of the framework level is designed to be optional and replaceable.

#### Embedder.
- To the underlying operating system, Flutter applications are packaged in the same way as any other native application. A platform-specific embedder provides an entrypoint; coordinates with the underlying operating system for access to services like rendering surfaces, accessibility, and input; and manages the message event loop. The embedder is written in a language that is appropriate for the platform: currently Java and C++ for Android, Objective-C/Objective-C++ for iOS and macOS, and C++ for Windows and Linux. Using the embedder, Flutter code can be integrated into an existing application as a module, or the code may be the entire content of the application. Flutter includes a number of embedders for common target platforms, but other embedders also exist.

#### Engine.
- At the core of Flutter is the Flutter engine, which is mostly written in C++ and supports the primitives necessary to support all Flutter applications. The engine is responsible for rasterizing composited scenes whenever a new frame needs to be painted. It provides the low-level implementation of Flutter’s core API, including graphics (through Impeller on iOS and coming to Android, and Skia on other platforms) text layout, file and network I/O, accessibility support, plugin architecture, and a Dart runtime and compile toolchain.
- The engine is exposed to the Flutter framework through dart:ui, which wraps the underlying C++ code in Dart classes. This library exposes the lowest-level primitives, such as classes for driving input, graphics, and text rendering subsystems.

#### Framework.
- Typically, developers interact with Flutter through the Flutter framework, which provides a modern, reactive framework written in the Dart language. It includes a rich set of platform, layout, and foundational libraries, composed of a series of layers. Working from the bottom to the top, we have:

- Basic foundational classes, and building block services such as animation, painting, and gestures that offer commonly used abstractions over the underlying foundation.
- The rendering layer provides an abstraction for dealing with layout. With this layer, you can build a tree of renderable objects. You can manipulate these objects dynamically, with the tree automatically updating the layout to reflect your changes.
- The widgets layer is a composition abstraction. Each render object in the rendering layer has a corresponding class in the widgets layer. In addition, the widgets layer allows you to define combinations of classes that you can reuse. This is the layer at which the reactive programming model is introduced.
- The Material and Cupertino libraries offer comprehensive sets of controls that use the widget layer’s composition primitives to implement the Material or iOS design languages.
- The Flutter framework is relatively small; many higher-level features that developers might use are implemented as packages, including platform plugins like camera and webview, as well as platform-agnostic features like characters, http, and animations that build upon the core Dart and Flutter libraries. Some of these packages come from the broader ecosystem, covering services like in-app payments, Apple authentication, and animations.


### 1- What is a typedef ?
- In Dart , typedef or (function types alias) helps to define pointer to excute code within memory.
- typedef can be used as a pointer that references a function.
- It is a type alias allows you to provide a new name for an existing data type into your program.
- Type alias don't create a new types , they simply provide a new name to an existing type.
```
typedef IntList=List<int>;
IntList il=[1,2,3];
```
### 2- Difference between const and final ?

#### final.
- allows only a single assignment.
- It must have an initializer.
- once it has been initialized with a value, the variable cannot be reassigned.
- A final variable may rely on runtime excution of code to determine its state, but it must occur during initialization.
- :thumbsup:
    ```
  final Datetime datetime=Datetime.now();
  ```
#### const.
- are compile time const.
- A Constant's entire deep state must be determinable at compile time.
- the const value will be frozen and immutable while the program is running.
- :thumbsdown:
    ```
    const Datetime datetime=Datetime.now();     xxxxxx
    ```

### 3- Does Dart Single threaded language and why ?
   - Yes, Dart is a single threaded language .
   - Because it use only one thread.
   - It excutes one thing at a time with the support of isolates , event loop and asynchronous code.
   - The event loop handles the excution of multiple chunks of your program over time.
   - the event loop is what allows multiple operations in a non-blocking way.
   
### 4- What is the use of private keyword in dart ?
   - Private keyword doesn't exist in dart.
   - We use underScore before the variable name instead of private.
   - It is used for encapsulating and securing your code, It makes it accessible only within their respective classes or libraries.

### 5- What is the meaning of immutable ?
- immutable constructs that cannot be mutated (altered) after they have been initialized.
- Strings, numbers and boolean can't be mutated.
- a String variable doesn't contain data itself, it is a reference to the string data's location in memory.
- non final string variables can be reassigned.

#### advantages of using immutable data.
- it's inherently thread safe, because since no code can alter its content , it is guaranted to the same reference no matter what code is accessing it.

### 6- What is a singleton ?
- Singleton pattern ensures that a class has only one instance and also provides a global point of access to it.
```
class Singleton {
  static final Singleton _singleton = Singleton._internal();

  factory Singleton() {
    return _singleton;
  }

  Singleton._internal();
}

main() {
  var s1 = Singleton();
  var s2 = Singleton();
  print(identical(s1, s2));  // true
  print(s1 == s2);           // true
}
```
### 7- What is isolate in dart ?
- An isolate in Dart is an independent unit of execution that runs concurrently in a separate memory heap.
- It allows for parallel processing and better utilization of multi-core systems.
- Isolates don't share memory; they communicate with each other by passing messages (usually immutable data) using ports.
- This approach helps to avoid common issues related to shared-memory concurrency, like race conditions or deadlocks.
- Each isolate has its own event queue and event loop, which processes incoming messages and ensures that only one message is handled at a time, preserving sequential consistency within the isolate.

### 8- Difference between function and method ?
#### function.
- is a top-level function which is declared outside of a class or an inline function.
- doesn't need an object as independent.

#### method.
- is tied to an instance of a class and has an implicit reference to  this.
- is a function which is linked with an object
- we call it by the object's name.

### 9- What is a sealed class ?
- Can't be extended outside of its library "file".

### 10- What is an inhereted widget in flutter ?
- Base class of widgets that efficiently propaget information down the tree ( Scaffold, Theme ).

### 11- Difference between var and dynamic ?
#### var.
- can't change TYPE of the variable.
- but can change the VALUE of the variable later in code.

#### dynamic.
- can change TYPE of the variable.
- can change VALUE of the variable later in code.

### 12- Difference between Visibility, Opacity & OffStage ?
#### Visibility.
- Visibility widget is to show/hide widgets.
- it has a visible property, which helps us in showing or hiding child.
- when visible is set to false, the actual child is replaced with zero- sized box instead.
```
// manage visibility
              Visibility(
                 
                // showing the child widget
                visible: true, // true to show, false to hide
                child: Text(
                  "Visible/Hide Text Example",
                  
                ),
              ),
```
#### Opacity.
- The opacity widget in flutter is used to make it’s child transparent.
- it can be done by using opacity property and set it 0, (range 0.0 - 1.0).
- The child is completely invisible when set to opacity 0, but will acquire the space & widget is also interactive.
```
Opacity(
  opacity: _visible ? 1.0 : 0.0,
  child: const Text("Now you see me, now you don't!"),
)
```
#### OffStage.
- OffStage in flutter widget lays it child out, as if it in true but don’t draw/render the child widget view on screen, and all don’t take space of screen.
- most of the time offstage is used to measure the dimension of widget without showing it on screen.
```
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  static const String _title = 'Flutter Code Sample';

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: _title,
      home: Scaffold(
        appBar: AppBar(title: const Text(_title)),
        body: const Center(
          child: MyStatefulWidget(),
        ),
      ),
    );
  }
}

class MyStatefulWidget extends StatefulWidget {
  const MyStatefulWidget({Key? key}) : super(key: key);

  @override
  State<MyStatefulWidget> createState() => _MyStatefulWidgetState();
}

class _MyStatefulWidgetState extends State<MyStatefulWidget> {
  final GlobalKey _key = GlobalKey();
  bool _offstage = true;

  Size _getFlutterLogoSize() {
    final RenderBox renderLogo =
        _key.currentContext!.findRenderObject()! as RenderBox;
    return renderLogo.size;
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        Offstage(
          offstage: _offstage,
          child: FlutterLogo(
            key: _key,
            size: 150.0,
          ),
        ),
        Text('Flutter logo is offstage: $_offstage'),
        ElevatedButton(
          child: const Text('Toggle Offstage Value'),
          onPressed: () {
            setState(() {
              _offstage = !_offstage;
            });
          },
        ),
        if (_offstage)
          ElevatedButton(
              child: const Text('Get Flutter Logo size'),
              onPressed: () {
                ScaffoldMessenger.of(context).showSnackBar(
                  SnackBar(
                    content:
                        Text('Flutter Logo size is ${_getFlutterLogoSize()}'),
                  ),
                );
              }),
      ],
    );
  }
}
```
### 13- Difference between Expanded and Flexible ?
- Flexible takes only the needed space, and Expanded takes all available space, respecting the flex factor.
- The Expanded widget simply takes all available space.
- One important distinction between the Flexible and Expanded widgets is that Flexible does not force its children to take the same size as itself where the Expanded widget forces its child to take the same size.
- Widget under Flexible are by default WRAP_CONTENT although you can change it using parameter fit.
- Widget under Expanded is MATCH_PARENT you can change it using flex.

### 14- What id generic programming ?
- Style of computer programming in which algorithims are written in terms of types to be specified later that are then instantiated when needed for specific types provided.

### 15- Solid Principles ?

#### S=> Single responsibility principle .
- A class should only be responsible for one thing that means a class could change for one reason.

#### O=> Opened-Closed Principle .
- An entity should be open for extension but closed for modification.
- Adding new features without modifying the existing code.

#### L=>Liskov substitution principle.
- Objects of a superclass should be replacable with objects of its subclass without breaking the application.
- Objects of our subclass behaves the same way as objects of our superclass.

#### I=>Interface Segregation Principle .
- It states that no client should be forced to depend on methods it does not use.
- Client should never depend on any thing more than the method it's calling.

#### D=>Dependency inversion principle .
- Abstractions should not depend on details (Concrete implementations), they should depend on abstractions.
- You will be able to change the implementation without altering the high level code.
- Depending on abstractions gives the freedom to be independent of the implementations.

### 16- What is Records in dart ?
- Records are an anonymous, immutable, aggregate type. Like other collection types, they let you bundle multiple objects into a single object. Unlike other collection types, records are fixed-sized, heterogeneous, and typed.
- Records are real values; you can store them in variables, nest them, pass them to and from functions, and store them in data structures such as lists, maps, and sets.
```
var record = ('first', a: 2, b: true, 'last');
```
### 17- What is the difference between .map() and .foreach() methods in Dart while iterating over an array ?
- The major difference is forEach doesn't returns anything while map() does return another array which satisfies the conditions.
- forEach iterates over each element in the array, it's a function which won't return.
```
xyz = [1,2,3,4,5]

newArray = xyz.map( (x) => x == 3)

xyz.forEach( (x) {  
if(x == 3) print("Yo"); 
})
```
### 18- What is Spread Operator and Null-aware Spread Operator in dart ?
- In Dart, Spread Operator (…) and Null-aware Spread Operator (…?) are used for inserting multiple elements in a collection like Lists, Maps, etc.
- Spread Operator.
```
...Data_structure
```
- Null-aware Spread operator.
```
...?Data_structure
```
```
void main() { 
  
   // initialise a List l1 
   List? l1 = ["Geeks","For","Geeks"]; 
    
  // initialize another List l2 using l1 
  List? l2=["Wow",...l1,"is","amazing"]; 
  
   // print List l2 
   print(l2); 
}
```
### 19- Difference between .then() and .whenCompleted() methods when working with Futures ?
- .whenComplete will fire a function either when the Future completes with an error or not, instead .then will fire a function after the Future completes without an error.
- catchError runs if the future fails.
```
someFuture().then((value) {
  print('Future finished successfully i.e. without error');
}).catchError((error) {
  print('Future finished with error');
}).whenComplete(() {
  print('Either of then or catchError has run at this point');
});
```
### 20- What is a mixin class in dart ?
- A way of defining code that can be reused in multiple class hierarchies.
```
mixin Mixin{}

class Me extends Person with Mixin{}
```
### 21- What is a stream in dart ?
- Define asynchronous programming in dart.
- A stream can be thought of as series of asynchronous occurance.
- Could be thought of as a pipe and the water inside it is the data.

### 22- Explain OOP principles in programming ?
#### Abstraction.
- The process of hiding the internal data and implementation details from the outer world.
- Its used to describe things in simple terms.
- It's used to create a boundary between the application and the client programs.
##### Abstract class.
- Cannot be instantiated and can contain abstract and non-abstract methods.
##### Interface class.
- Specifies a set of methods that a class must implement.
##### Benefits.
- Reduces boilerplate code (Code sections repeated throughout a program or software).
- Increase reuseability, maintainability and readability.
 
<br/>

#### Inheritance.
- One class inherits the attributes and methods of another class.
- Child class from parent class.

##### Benefits.
- Code reusability, save time and reduce code boilerplate.

##### Types.
- Single Inheritence.
- Multiple Inheritence (Dart doesn't support multiple inheritence but we can use mixins to inherit multiple classes).
- Multilevel Inheritence.

<br/>

#### Polymorphism.
- Multi form => the concept that you can access objects of different types through the same interface.
- The ability of any data to be processed in more than one form.
- the ability of an object to take many forms.
- Allows to compensate any reference of the super class by any object of the sub class.
- Allows to perform a single action in different ways.
- Reduces Coupling.
- Increase Reusability.
```
abstract class Person{}
class Me extends Person{}
class Him extends Person{}

Person me=new Me();

Person him=new Him();
```
<br/>

#### Encapsulation.
- bundling of data and methods that operate on that data within single unit (class).
- The method of hiding the implementation details of a class from outside access and only exposing a public interface.
- It's a protective shield that prevent data from being accessed by code outside this shield.
- In dart we use _var instead of private keyword.
- Getters => Read only.
- Setters => Write only.

##### Benefits.
- Data Hiding, increases flexibility and reusability.

### 23- Introduce the Class modifiers in dart "3"! ?

#### No modifier.

##### To allow unrestricted permission to construct or subtype from any library, use a class or mixin declaration without a modifier. By default, you can:
- Construct new instances of a class.
-  Extend a class to create a new subtype.
-  Implement a class or mixin’s interface.
-  Mix in a mixin or mixin class.


#### abstract.
- To define a class that doesn’t require a full, concrete implementation of its entire interface, use the abstract modifier.
- Abstract classes cannot be constructed from any library, whether its own or an outside library. Abstract classes often have abstract methods.
- If you want your abstract class to appear to be instantiable, define a factory constructor.
```
// Library a.dart
abstract class Vehicle {
  void moveForward(int meters);
}

// Library b.dart
import 'a.dart';

// Error: Cannot be constructed
Vehicle myVehicle = Vehicle();

// Can be extended
class Car extends Vehicle {
  int passengers = 4;
  // ···
}

// Can be implemented
class MockVehicle implements Vehicle {
  @override
  void moveForward(int meters) {
    // ...
  }
}
```

#### base.
##### To enforce inheritance of a class or mixin’s implementation, use the base modifier. A base class disallows implementation outside of its own library. This guarantees:
- The base class constructor is called whenever an instance of a subtype of the class is created.
- All implemented private members exist in subtypes.
- A new implemented member in a base class does not break subtypes, since all subtypes inherit the new member. This is true unless the subtype already declares a member with the same name and an incompatible signature.
- You must mark any class which implements or extends a base class as base, final, or sealed. This prevents outside libraries from breaking the base class guarantees.

```
// Library a.dart
base class Vehicle {
  void moveForward(int meters) {
    // ...
  }
}

// Library b.dart
import 'a.dart';

// Can be constructed
Vehicle myVehicle = Vehicle();

// Can be extended
base class Car extends Vehicle {
  int passengers = 4;
  // ...
}

// ERROR: Cannot be implemented
base class MockVehicle implements Vehicle {
  @override
  void moveForward() {
    // ...
  }
}
```

#### interface.
##### To define an interface, use the interface modifier. Libraries outside of the interface’s own defining library can implement the interface, but not extend it. This guarantees:
- When one of the class’s instance methods calls another instance method on this, it will always invoke a known implementation of the method from the same library.
- Other libraries can’t override methods that the interface class’s own methods might later call in unexpected ways. This reduces the fragile base class problem.
```
// Library a.dart
interface class Vehicle {
  void moveForward(int meters) {
    // ...
  }
}

// Library b.dart
import 'a.dart';

// Can be constructed
Vehicle myVehicle = Vehicle();

// ERROR: Cannot be inherited
class Car extends Vehicle {
  int passengers = 4;
  // ...
}

// Can be implemented
class MockVehicle implements Vehicle {
  @override
  void moveForward(int meters) {
    // ...
  }
}
```

#### abstract interface.
- The most common use for the interface modifier is to define a pure interface. Combine the interface and abstract modifiers for an abstract interface class.
- Like an interface class, other libraries can implement, but cannot inherit, a pure interface. Like an abstract class, a pure interface can have abstract members.

<br/>

#### final.
#### To close the type hierarchy, use the final modifier. This prevents subtyping from a class outside of the current library. Disallowing both inheritance and implementation prevents subtyping entirely. This guarantees:

- You can safely add incremental changes to the API.
- You can call instance methods knowing that they haven’t been overwritten in a third-party subclass.
- Final classes can be extended or implemented within the same library. The final modifier encompasses the effects of base, and therefore any subclasses must also be marked base, final, or sealed.

```
// Library a.dart
final class Vehicle {
  void moveForward(int meters) {
    // ...
  }
}

// Library b.dart
import 'a.dart';

// Can be constructed
Vehicle myVehicle = Vehicle();

// ERROR: Cannot be inherited
class Car extends Vehicle {
  int passengers = 4;
  // ...
}

class MockVehicle implements Vehicle {
  // ERROR: Cannot be implemented
  @override
  void moveForward(int meters) {
    // ...
  }
}

```
#### sealed.
- To create a known, enumerable set of subtypes, use the sealed modifier. This allows you to create a switch over those subtypes that is statically ensured to be exhaustive.

#### The sealed modifier prevents a class from being extended or implemented outside its own library. Sealed classes are implicitly abstract.

- They cannot be constructed themselves.
- They can have factory constructors.
- They can define constructors for their subclasses to use.
- Subclasses of sealed classes are, however, not implicitly abstract.

- The compiler is aware of any possible direct subtypes because they can only exist in the same library. This allows the compiler to alert you when a switch does not exhaustively handle all possible subtypes in its cases:
```
sealed class Vehicle {}

class Car extends Vehicle {}

class Truck implements Vehicle {}

class Bicycle extends Vehicle {}

// ERROR: Cannot be instantiated
Vehicle myVehicle = Vehicle();

// Subclasses can be instantiated
Vehicle myCar = Car();

String getVehicleSound(Vehicle vehicle) {
  // ERROR: The switch is missing the Bicycle subtype or a default case.
  return switch (vehicle) {
    Car() => 'vroom',
    Truck() => 'VROOOOMM',
  };
}
```
- If you don’t want exhaustive switching, or want to be able to add subtypes later without breaking the API, use the final modifier.

### 24- What is Enum ?
- Enum stands for enumerated type, a type of data where only a set of predefined values exist.
- In Dart, Enum is simply a special kind of class used to represent a fixed number of constant values.
- All enums automatically extend the Enum class. They are also sealed, meaning they cannot be subclassed, implemented, mixed in, or otherwise explicitly instantiated.
- Abstract classes and mixins can explicitly implement or extend Enum, but unless they are then implemented by or mixed into an enum declaration, no objects can actually implement the type of that class or mixin.

```
enum OperatingSystem { macOS, windows, linux }
```

### 25- Difference Override and overload in programming ?
- Firstly, Dart doesn't support overloading.
- Overriding occurs when the method signature is the same in the superclass and the child class. 
- Overloading occurs when two or more methods in the same class have the same name but different parameters.
- Method overloading deals with the notion of having two or more methods in the same class with the same name but different arguments.
```
void foo(int a)
void foo(int a, float b)
```
- Method overriding means having two methods with the same arguments, but different implementations. One of them would exist in the parent class, while another will be in the derived, or child class. The @Override annotation, while not required, can be helpful to enforce proper overriding of a method at compile time.
```
class Parent {
    void foo(double d) {
        // do something
    }
}

class Child extends Parent {

    @Override
    void foo(double d){
        // this method is overridden.  
    }
}
```

### 26- Extenstions in dart?
### 27- Named Constructor?
### 28- Factory constructor?
### 29- Design patterns?
### 30- Iterables?
### 31- this keyword?
### 32- Types of streams?
### 33- Get, Post, Delete, update?
### 34- Blocprovider, bloclistener, blocbuilder?
### 35- listview, listview.builder?
### 36- AssetImage, Image.asset?
### 37- What Does WidgetsFlutterBinding.ensureInitialized() do ?
- The WidgetFlutterBinding is used to interact with the Flutter engine.
- Ex. Firebase.initializeApp() needs to call native code to initialize Firebase, and since the plugin needs to use platform channels to call the native code, which is done asynchronously therefore you have to call ensureInitialized() to make sure that you have an instance of the WidgetsBinding.
- Returns an instance of the WidgetsBinding, creating and initializing it if necessary. If one is created, it will be a WidgetsFlutterBinding. If one was previously initialized, then it will at least implement WidgetsBinding.
- You only need to call this method if you need the binding to be initialized before calling runApp.
```
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}
```
