Java Quick Reference for C# Developers
======================================


#### Naming Conventions

Interfaces (Prefixed with `I` vs. not):

```
C#: 
interface IAction 

Java: 
interface Action
```

Methods (Pascal vs. camel case):

```
C#:
public void DoSomething();

Java:
public void doSomething();
```

Braces (BSD style vs. K&R style):

```
C#:
public bool Equals(int a, int b)
{
    if (a == b)
    {
        return true;
    }
    else 
    {
        reutrn false;
    }
}

Java:
public boolean equals(int a, int b) {
    if (a == b){
        return true;
    } else {
        return false;
    }
}
```

#### Types

|Java    |C#      |CLR Type|
|--------|--------|--------|
|String  |string  |String  |
|Object  |object  |Object  |
|boolean |bool    |Boolean |
|char    |char    |Char    |
|short   |short   |Int16   |
|int     |int     |Int32   |
|long    |long    |Int64   |
|double  |double  |Double  |
|float   |float   |Single  |
|byte    |sbyte   |SByte   |
|-       |byte    |Byte    |
|-       |ushort  |UInt16  |
|-       |uint    |UInt32  |
|-       |ulong   |UInt64  |

Get type of an object:
|C#            |Java        |
|--------------|------------|
|`typeof(Foo)` |`Foo.class` |

Check if an object is compatible with a given type:

|C#              |Java                    |
|----------------|------------------------|
|`obj is String` |`obj instanceof String` |

#### Namespaces and Packages

```
C#
namespace Microsoft.Protocols;

Java:
package com.microsoft.protocols;
```

#### Constants

```
C#:
const double pi = 3.1415926;

Java:
final double PI = 3.1415926;
```

```
C#:
static readonly string name = "Tom";

Java:
final string name = "Tom";
```

#### For-each Loops

```
C#:
foreach(T item in items) { ... }

Java:
for(T item : items) { ... }
```

#### Access Modifiers

Java does not have `internal` keyword. Non-public classes are visible within package.

|C#        |Java      |
|----------|----------|
|public    |public    |
|protected |protected |
|private   |private   |
|internal  |-         |


#### Structs

C# has reference and value types; Java has reference and primitive type.
In C# you can use `struct` to create custom value types. Java does not have `struct`.

```
C#:
public struct Point {
    public int X;
    public int Y;
}
```

#### Enums

Java Enums have much richer features than C#. You can define methods in Enums. And Enums can inherit from other classes or interfaces.

```
C#:
enum DeviceTypes {
    Android,
    Windows,
    WindowsRT
// you cannot do anything else
}

Java:
enum DeviceTypes implements Runnable {
// Enum in Java can implement interfaces or inherit classes
    Android,
    Windows,
    WindowsRT
    
    // you can define methods in an enum
    @Override
    public void run() {
        System.out.println("Enum in Java implement interfaces");
   }
}
```

#### Nested Classes

C# and Java both have inner classes, but they behave differently. Java implicitly passes a reference to an instance of the outer class to the inner class, allowing the inner class to access fields of the outer class. C# inner classes do not have the similar functionality.

```
C#:
class OuterClass {
    string field;
    
    class InnerClass {
    
        void Method(){
            Console.WriteLine(field) ; // Error!
        }
        
    }
}

Java:
class OuterClass {
    string field;
    
    class InnerClass {
    
        void method(){
            System.out.println(field); // OK!
        }
        
    }
}
```

#### Properties

Java does not have properties. 

```
C#
class Person {
    private string name;

    public string Name {
        get { return name; }
        set { name = value;}
    }
}

Java:
class Person {
    private string name;
    
    public string getName() {
        return name;
    }
    
    public void setName(string name) {
        this.name = name;
    }
}
```


#### Override

All methods are overridable, except those marked with `final`.
Java does not have `override` keyword. 

```
C#:
class Parent {
    // methods with virtual keyword can be override
    public virtual void Method1() { ... }
    
    // methods without virtual keyword cannot be overrided
    public void Method2() { ... }
}

class Child : Parent {
    // use override keyword when overriding a parent method
    public override void Method1() { ... }
}

Java:
class Parent {
    // all methods are overridable by default
    public void method1() { ... }
    
    // method with final cannot be overrided
    public final void method2() { ... }
}

class Child extends Parent {
    @Override
    public void method1() { ... }
}
```

#### Generics

C# uses reified generics. Generics are a runtime feature. While Java uses type erasure. Generics are (mostly) a compiler feature.

```
C#:
new List<int>().GetType(); // List`1[Int32]

Java:
new ArrayList<Integer>().getClass(); // ArrayList
```

Generic methods:

```
C#:
public class ListFactory {
    public static IList<T> CreateList<T>() {
        return new List<T>();
    }
}

IList<String> list = ListFactory.CreateList<String>();

Java:
public class ListFactory {
    public static <T> List<T> createList() {
        return new ArrayList<T>();
    }
}

List<String> list = ListFactory.createList();
```

Constraints:

```
C#:
T Max<T>(T a, T b) where T: IComparable<T> {
    if (a.CompareTo(b) > 0) return a;
    else return b;
}

Java:
<T extends Comparable<T>> T max(T a, T b) {
    if (a.compareTo(b) > 0) return a;
    else return b;
}
```

Constrain Keywords:
|C#                         |Java                        |Meaning                             |
|---------------------------|----------------------------|------------------------------------|
|`where T: IComparable<T>`  | `T extends Comparable<T>`  |                                    |
|`where T: new()`           | -                          | T has a parameterless constructor. |
|`where T: class`           | -                          | T is a reference type.             |
|`where T: struct`          | -                          | T is a value type.                 |




#### Delegates and Events

Java does not have delegates or events. Callbacks are implemented using interfaces and anonymous classes. 

```
C#
delegate void OnInvoked(string msg);

static void Print(OnInvoked callback) {
    callback("Hello World!");
}

static void Main(string[] args) {
    Print(delegate(string msg) {
        Console.WriteLine(msg);
    });
}

Java:
interface OnInvoked{
    void onInvoked(String msg);
}

static void print(OnInvoked callback){
    callback.onInvoked("Hello World!");
}

static void main(String[] args){
    print(new OnInvoked(){
        @Override
        public void onInvoked(String msg){
            System.out.println(msg);
        }
    });
}
```

#### Attributes

Java **annotations** function similarly as attributes in C#.

```
C#
[AttributeUsage(AttributeTargets.Class)]
public class MyAttribute : Attribute {
    public string Name;
    public string Value;
}

[MyAttribute(Name="SomeName",Value="SomeValue")]
public class TheClassWithMyAttribute {
    ...
}

Java 5:
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface MyAnnotation {
    public String name();
    public String value();
}

@MyAnnotation(name="SomeName",  value = "SomeValue")
public class TheClassWithMyAttribute {
    ...
}
```

#### Reflections

Both C# and Java supports powerful and easy-to-use reflection operations.

```
C#:
var attribute = typeof(TheClass).GetCustomAttributes(typeof (MyAttribute), true);

Java:
Annotation annotation = TheClass.class.getAnnotation(MyAnnotation.class);
```

#### Exceptions


```
C#:
// everything thrown is an instance of Exception
catch (Exception e) {
    throw e; // re-throw with throw e
}

Java
// everything thrown is an instance of Throwable
catch (Throwable t) {
    throw; // re-throw with throw
}
```

#### Checked and Unchecked Exceptions

C# does not have checked exceptions. Java has checked and unchecked exceptions.

Unchecked exceptions:

* represent defects in the program (invalid arguments, null pointers)
* are subclasses of `java.lang.RuntimeException`
* not required to be handled
* examples:  `IllegalArgumentException`, `NullPointerException`

Checked exceptions:

* represent invalid conditions in areas outside the immediate control of the program (invalid user input, database problems, network outages, absent files)
* are subclasses of `java.lang.Exception`
* must be caught or explicitly declared thrown
* examples: `IOException`,`FileNotFoundException`

```
Java:
// throws unchecked exception
void methodThrowsUncheckedException() {
    throw new IllegalArgumentException();
}

static void main(String[] args) {
    // not required to be caught
    methodThrowsUncheckedException();
}

// throws checked exception
void methodThrowsCheckedException() throws IOException {
    throw new IOException();
}

static void main(String[] args)
    try {
        methodThrowsCheckedException();
    } catch(IOException e) {
        // required to be handled
        // or declared as thrown
    }
}
```
#### _using_ blocks

**Java 7** as "Automatic Resource Management" (ARM) using the `try` keyword.

```
C#:
using(StreamReader reader = new StreamReader(new FileStream(path))) {
  ...
}

Java 7:
try (BufferedReader reader = new BufferedReader(new FileReader(path))) {
   ...
}
```


#### Lambda Expressions

Lambda expression is introduced in **Java 8**.
```
C#:
Task.Run(
    () => Console.WriteLine("Hello from thread");
);

Java 8:
new Thread(
    () -> System.out.println("Hello from thread")
).start();
```

#### LINQ

**Java 8** introduces `stream`, which is kind of an equivalent to LINQ.

```
C#:
List<int> list = new List<int>{1,2,3,4,5,6,7};
int sum = list.Select(x => x*x).Aggregate((x,y) => x + y);

Java 8:
List<Integer> list = Arrays.asList(1,2,3,4,5,6,7);
int sum = list.stream().map(x -> x*x).reduce((x,y) -> x + y).get();

```

#### Specific Features of _C#_

The following features in C# do no have any equivalent in Java:

* Operator overloading
* `dynamic` type
* `var` keyword
* `yield` keyword
* `out` parameter
* Extension methods
* Expression trees
* Explicit interfaces
* Partial classes
* ...

See here for a [Full list of comparision between C# and Java](http://en.wikipedia.org/wiki/Comparison_of_C_Sharp_and_Java) on Wikipedia.



