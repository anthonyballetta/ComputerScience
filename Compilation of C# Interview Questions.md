# 1. What is an extension method?

An extension method enables us to add methods to existing types without creating a new derived type, recompiling, or modify the original types. We can say that it extends the functionality of an existing type in .NET. An extension method is a static method to the existing static class. We call an extension method in the same general way; there is no difference in calling. It uses the "this" keyword as the first parameter with a type in .NET and this method will be called by a given type instance on the client side.

# 2. What is an interface class?  

Interface is an abstract class which has only public abstract methods and the methods only have the declaration and not the definition. These abstract methods must be implemented in the inherited classes.

# 3. What is multiple inheritance?

Multiple inheritance is a feature of some object-oriented computer programming languages in which an object or class can inherit characteristics and features from more than one parent object or parent class.

# 4. What is an interface in C#?

An interface looks like a class, but has no implementation. The only thing it contains are declarations of events, indexers, methods and/or properties. The reason interfaces only provide declarations is because they are inherited by classes and structs, which must provide an implementation for each interface member declared. C# does not support multiple inheritance so interfaces were created to solve this problem. 

#### Implementation Example

Lets take the idea of a pizza ordering service. You can have multiple types of pizzas and a common action for each pizza is preparing the order in the system. Each pizza has to be prepared but each pizza is prepared differently. For example, when a stuffed crust pizza is ordered the system probably has to verify certain ingredients are available at the restaurant and set those aside that aren't needed for deep dish pizzas.

When writing this in code, technically you could just do
```
public class Pizza()
{
    public void Prepare(PizzaType tp)
    {
        switch (tp)
        {
            case PizzaType.StuffedCrust:
                // prepare stuffed crust ingredients in system
                break;

            case PizzaType.DeepDish:
                // prepare deep dish ingredients in system
                break;

            //.... etc.
        }
    }
}
```

However, deep dish pizzas (in C# terms) may require different properties to be set in the Prepare() method than stuffed crust, and thus you end up with a lot of optional properties, and the class doesn't scale well (what if you add new pizza types).

The proper way to solve this is to use interface. The interface declares that all Pizzas can be prepared, but each pizza can be prepared differently. So if you have the following interfaces:
```
public interface IPizza
{
    void Prepare();
}

public class StuffedCrustPizza : IPizza
{
    public void Prepare()
    {
        // Set settings in system for stuffed crust preparations
    }
}

public class DeepDishPizza : IPizza
{
    public void Prepare()
    {
        // Set settings in system for deep dish preparations
    }
}
```
Now your order handling code does not need to know exactly what types of pizzas were ordered in order to handle the ingredients. It just has:
```
public PreparePizzas(IList<IPizza> pizzas)
{
    foreach (IPizza pizza in pizzas)
        pizza.Prepare();
}
```
Even though each type of pizza is prepared differently, this part of the code doesn't have to care what type of pizza we are dealing with, it just knows that it's being called for pizzas and therefore each call to Prepare will automatically prepare each pizza correctly based on its type, even if the collection has multiple types of pizzas.

# 5. What is a static method?
A static function, unlike a regular (instance) function, is not associated with an instance of the class.

A static class is a class which can only contain static members, and therefore cannot be instantiated.
For example:
```
class SomeClass {
    public int InstanceMethod() { return 1; }
    public static int StaticMethod() { return 42; }
}
In order to call InstanceMethod, you need an instance of the class:
SomeClass instance = new SomeClass();
instance.InstanceMethod();   //Fine
instance.StaticMethod();     //Won't compile

SomeClass.InstanceMethod();  //Won't compile
SomeClass.StaticMethod();    //Fine
```

# 6. What is the new operator? 
The new operator creates an instance of an class.

# 7. What is the ‘this’ keyword?
The ‘this’ keyword is a reference to the current object.	

# 8. What does immutable mean? 
Mutable can be changed, Immutable can’t be changed. String is standard immutable, StringBuilder is mutable string type.

# 9. Array vs ArrayList vs List?

An Array (System.Array) is fixed in size once it is allocated. You can't add items to it or remove items from it. Also, all the elements must be the same type. As a result, it is type safe, and is also the most efficient of the three, both in terms of memory and performance. Also, System.Array supports multiple dimensions (i.e. it has a Rank property) while List and ArrayList do not (although you can create a List of Lists or an ArrayList of ArrayLists, if you want to).

An ArrayList is a flexible array which contains a list of objects. You can add and remove items from it and it automatically deals with allocating space. If you store value types in it, they are boxed and unboxed, which can be a bit inefficient. Also, it is not type-safe.
A List<> leverages generics; it is essentially a type-safe version of ArrayList. This means there is no boxing or unboxing (which improves performance) and if you attempt to add an item of the wrong type it'll generate a compile-time error.

# 10. How can you sort the elements of an array in descending order?

By calling Array.Sort() and then Array.Reverse() methods.

# 11. Can you prevent your class from being inherited by another class?

Yes, the keyword 'sealed' will prevent this method from being inherited.

# 12. What is method overloading, what is method overriding?

Overloading is when you have multiple methods in the same scope, with the same name but different signatures.

Overriding is a principle that allows you to change the functionality of a method in a child class.

#### Implementation examples
```
//Overloading
public class test
{
    public void getStuff(int id)
    {}
    public void getStuff(string name)
    {}
}

//Overriding
public class test
{
        public virtual void getStuff(int id)
        {
            //Get stuff default location
        }
}

public class test2 : test
{
        public override void getStuff(int id)
        {
            //base.getStuff(id);
            //or - Get stuff new location
        }
}
```
# 12. What are the different ways a method can be overloaded?

Different parameter data types, different number of parameters, different order of parameters.

# 13. What are the different types of errors?

Syntax error. This type of error, which is identified during compilation, occurs because the programmer has used syntax incorrectly or included a typo in the code.

Logic error. This type of error causes the program to do something other than what the programmer intended. The program will output an unexpected result in response to tests.

Runtime error. This type of error causes the program to crash or terminate incorrectly.

# 14. What is the difference between a struct and a class?

Structs cannot be inherited. Structs are passed by value and not by reference. Structs are stored on the stack not the heap. The result is better performance with Structs.

# 15. What is Object oriented programming (OOP)?

OOP allows .NET developers to create classes containing methods, properties, fields, events and other logical modules. It also lets developers create modular programs, which they can assemble as applications. OOPs have four basic features: encapsulation, abstraction, polymorphism and inheritance.

# 16. What is encapsulation and abstraction? 

Abstraction is a process where you show only “relevant” data and “hide” unnecessary details of an object from the user. Consider your mobile phone, you just need to know what buttons are to be pressed to send a message or make a call, What happens when you press a button, how your messages are sent, how your calls are connected is all abstracted away from the user.

Encapsulation is the process of combining data and functions into a single unit called class. In Encapsulation, the data is not accessed directly; it is accessed through the functions present inside the class. In simpler words, attributes of the class are kept private and public getter and setter methods are provided to manipulate these attributes. Thus, encapsulation makes the concept of data hiding possible.

![Alt text](https://i.stack.imgur.com/L9iXI.png "Example")

# 17. Explain the concept of inheritance and how it works to .NET.

In general OOP terms, inheritance means that a class can be based on another class, with the child class taking on the attributes of the parent class. For example, coders can create a class called Vehicle, and then child classes called Truck, Car, Motorcycle — all of which inherit the attributes of Vehicle.

# 18. What is the difference between an abstract class and an interface?

An abstract class is always used as a base class. It provides some abstract/virtual members that the inheriting entities must implement, as well as a partial implementation for a functionality. For extra credit during a .NET interview, your candidate might mention that this class can also declare fields. Developers cannot create an object from this class.

# 19. What is the difference between a class and an object, and how do these terms relate to each other?

A class is a comprehensive data type that is the primary building block, or template, of OOP. Class defines attributes and methods of objects, and contains an object’s behavior and data. An object, on the other hand, represents an instance of class. As a basic unit of a system, objects have identity and behavior as well as attributes.

# 20. Explain the difference between a stack and a queue.

Stacks and queues are two examples of collections. (Hash tables, bags, dictionaries and lists also fall into this category.) A stack keeps track of what is executing and contains stored value types to be accessed and processed as LIFO (Last-In-First-Out), with elements inserted and deleted from the top end.

A queue, on the other hand, lists items on a FIFO (First-In-First-Out) basis in terms of both insertion and deletion, with items inserted from the rear end and deleting items from the front end of the queue.

# 21. What is .NET web service?

Web services are reusable components that allow developers to publish an application’s function over the internet to make it accessible and directly interactable with other applications and objects online. Web services communicate by using standard web protocols and data formats — including HTTP, XML and SOAP — that allow them to connect across different platforms and programming languages. ASP.NET provides a simple way to develop web services. The .NET framework provides built-in classes for building and consuming web services.

# 22. Define LINQ.

LINQ stands for Language Integrated Query. This is a Microsoft programming model and methodology that offers developers a way to manipulate data using a succinct yet expressive syntax. It does so by instilling Microsoft .NET-based programming languages with the ability to make formal queries. It is part of C# and can be imported as a library in other languages.

# 23. What do the terms “boxing” and “unboxing” mean?

This is one of those .NET interview questions that can reveal how much candidates know about data types and OOP principles. The idea is relatively simple: Boxing is a process that converts a value type to an object type — by “boxing” the variable inside a dedicated object or interface. Unboxing extracts this value and stores it in a value type. Boxing was essential in some old Collection types such as ArrayList, and can still be used for accurate conversion of types — for example, from a Double to an Int.

# 24. What are three of common acronyms used in .NET, and what do they stand for?

This one should be easy for .NET job candidates to answer, as long as they understand the basics. The interview question allows them some flexibility in choosing terms with which they are most familiar. Three frequently used acronyms in .NET are IL, CIL and CLI:

IL stands for Intermediate Language, which is an object-oriented programming language that is a partially compiled code that .NET developers will then compile to native machine code.

CIL stands for Common Intermediate Language, formerly known as Microsoft Intermediate Language (MSIL). This is another programming language that .NET developers use, and it represents the lowest possible level for a language that humans can still read.

CLI stands for Common Language Infrastructure. This is a compiled code library that Microsoft developed as an open specification. Developers use CLI for security, versioning and deployment purposes.

# 25. What is a constructor?

When a class or struct is created, its constructor is called. Constructors have the same name as the class or struct, and they usually initialize the data members of the new object.

In the following example, a class named Taxi is defined by using a simple constructor. This class is then instantiated with the new operator. The Taxi constructor is invoked by the new operator immediately after memory is allocated for the new object.

```
public class Taxi
{
    public bool isInitialized;
    public Taxi()
    {
        isInitialized = true;
    }
}

class TestTaxi
{
    static void Main()
    {
        Taxi t = new Taxi();
        Console.WriteLine(t.isInitialized);
    }
}
```
# 26. What is the difference between public, static and void?

You can access public declared variables anywhere in the application.

Static declared variables are globally accessible without creating an instance of the class.

Void is a type modifier that specifies that the method doesn't return any value.

# 27. What is a collection?

A collection works as a container for instances of other classes. All classes implement ICollection interface.

# 28. What is delegate in C#?

A delegate in C# is an object that holds the reference to a method. It is similar to function pointer in C++.

# 29. What is the purpose of the global.asax file?

Effectively, global.asax allows you to write code that runs in response to "system level" events, such as the application starting, a session ending, an application error occuring, without having to try and shoe-horn that code into each and every page of your site.

You can use it by by choosing Add > New Item > Global Application Class in Visual Studio. Once you've added the file, you can add code under any of the events that are listed (and created by default, at least in Visual Studio 2008):

Application_Start
Application_End
Session_Start
Session_End
Application_BeginRequest
Application_AuthenticateRequest
Application_Error
There are other events that you can also hook into, such as "LogRequest".

# 30. Difference between GET and POST.

GET requests data from a specified resource while POST submits data to be processed to a specific resource. 

Note that the query string (name/value pairs) is sent in the URL of a GET request:
```
/test/demo_form.php?name1=value1&name2=value2
```

Note that the query string (name/value pairs) is sent in the HTTP message body of a POST request:

```
POST /test/demo_form.php HTTP/1.1
Host: w3schools.com
name1=value1&name2=value2
```

# 31. Which is more secure between GET and POST?

POST is more secure than GET for a couple of reasons.

GET parameters are passed via URL. This means that parameters are stored in server logs, and browser history. When using GET, it makes it very easy to alter the data being submitted the the server as well, as it is right there in the address bar to play with.

The problem when comparing security between the two is that POST may deter the casual user, but will do nothing to stop someone with malicious intent. It is very easy to fake POST requests, and shouldn't be trusted outright.

The biggest security issue with GET is not malicious intent of the end-user, but by a third party sending a link to the end-user. I cannot email you a link that will force a POST request, but I most certainly can send you a link with a malicious GET request.

# 32. Difference between Server.Transfer and Response.Redirect

Response.Redirect should be used when:

we want to redirect the request to some plain HTML pages on our server or to some other web server
we don't care about causing additional roundtrips to the server on each request
we do not need to preserve Query String and Form Variables from the original request
we want our users to be able to see the new redirected URL where he is redirected in his browser (and be able to bookmark it if its necessary)

Server.Transfer should be used when:

we want to transfer current page request to another .aspx page on the same server
we want to preserve server resources and avoid the unnecessary roundtrips to the server
we want to preserve Query String and Form Variables (optionally)
we don't need to show the real URL where we redirected the request in the users Web Browser

# 33. What is a method?

A method is a code block that contains a series of statements. A program causes the statements to be executed by calling the method and specifying any required method arguments. In C#, every executed instruction is performed in the context of a method. The Main method is the entry point for every C# application and it is called by the common language runtime (CLR) when the program is started.

# 34. What is the difference between passing by value and by reference?

When an argument is passed by value (the default in C#), a copy of its value is made and passed to the called method. Changes to the copy do not affect the original variable’s value in the caller. This prevents the accidental side effects that so greatly hinder the development of correct and reliable software systems. Each argument that’s been passed in the programs so far has been passed by value. When an argument is passed by reference, the caller gives the method the ability to access and modify the caller’s original variable—no copy is passed.

A disadvantage of pass-by-value is that, if a large data item is being passed, copying that data can take a considerable amount of execution time and memory space.

# 35. What is a pointer? 

A pointer is a value that contains the memory address of another variable.

# 36. What are generics?

Generics refers to the technique of writing the code for a class without specifying the data type(s) that the class works on.

You specify the data type when you declare an instance of a generic class. This allows a generic class to be specialized for many different data types while only having to write the class once.

A great example are the many collection classes in .NET. Each collection class has it's own implementation of how the collection is created and managed. But they use generics to allow their class to work with collections of any type.
