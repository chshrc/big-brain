# Extbase

Notes accompanying notes for the book [TYPO3 Extbase, 3rd Edition](https://leanpub.com/typo3extbase-3rd-edition-en).

## Chapter 2 "PHP Programming Basics"

### OOP

In OOP the object does have attributes and function. The crucial part is to identify all those necessary attributes and functions. It might help to think of functions as ways to interact with an object. 
E.g. a light switch can be turned off or on and the attribute changing is the state "on/off".

In OOP the attributes are called "properties".

> # Hint
> The terms "fields", "properties", "attributes" and such are NOT canonical and can mean different things in different languages!
> E.g. Java reserves the term "property" for getters and setters of attributes/fields.

Class names in PHP use *UpperCamelCase*, properties and methods use *lowerCamelCase*.

The `new` operator creates an instance of a class, called an *Object*:
```php
$audi = new Car();
```
In PHP the name of the [*constructor*](Link to programming notes) is always `__construct`.

> Reminder: Parameters are the variables available for passing on to a function. Arguments are the actual values passed.
> That is:
> ```php
> public function __construct($colour) { $this->colour = $colour; }
> ```
> Here $colour is a parameter. Compare it to the following:
> ```php
> $bird = new Bird('red');
> ```
> Here 'red' is an argument.

To check which parent a subclass has, the keyword `instanceof` can be
used.
It will return a boolean.

If at least one method of a class is declared as `abstract`, the class is
considered an `abstract` class.
> Remember that abstract classes do not implement a body!
You use abstract classes if you know the class will be needed later but
the exact implementation details are not yet known by the time of
writing.

Using an `interface`, methods a class consists of can be defined in
advance. All classes defined in an `interface` need to be implemented in
the implementing classes. The methods in an interface need not be
declared by the keyword `abstract` (redundant as the interface states
that all methods need to be implemented).

> "The bottom line is that we can implement multiple classes at once but you
> can only derive (extend) from one
> class."

Regarding visibility of methods and properties:
"All properties in Extbase and Fluid are `protected` and all methods are
`public` (except internal methods)."

Similar to statically typed programming languages, type hints can be used
in PHP to only pass arguments of certain types as parameters to methods.
E.g.:
```php
public function rent(Car $vehicle)
{
	...
}
```
This way `$vehicles` must be of type `Car`.
> *Important*:
> Data types array and class names are valid type hints but standard
> types such as integer, string or boolean
> are not.

In a similar way, return type declarations can be used to define the type
of the return value of a method:
```php
public function toArray(int $a, int $b): array
{
	return [$a, $b];
}
```
A short way to indicate that the return value can be of type array or
`null` is to write `?array` (only PHP 7+).

Note, that the above code will *not* throw an error if the return value
type is not identical to the return type.

> *Important*:
> By default, PHP will coerce values of the wrong type into the expected
> scalar type if possible.
> That means, that return types will coerced to the declared type no
> matter what.
> To enable strict typing (since PHP 7+) on a per-file basis, add the
> following statement at the top of the file:
> ```php
> declare(strict_types=1)
> ```
> This will throw a TypeError if a variable not identical to the type
> declaration if passed.
>
> You *should* definitely use strict typing in all your TYPO3 extensions!

### 2.12
Class names beginning with a backslash \ tell PHP that the class name is a fully qualified class name (FQCN).
FQCN are usually the namespace + class name.

Using the `use` keyword you can create references to other FQCN outside of the current namespace of the class. Using `as` you can also give the reference an alias:
```php
namespace Book\Extbase\Code;
use Vehicle\Engine\FourWheels as FW;

class Car extends FW 
{
  ...
}
```

### 2.13

Design patterns are defined code structures to solve problems of a similar kind. That means the solution to e.g. dependency struggles in software development is using Dependency Injection.

In the book only three (out of mentioned ~80) are explained: Singleton, Prototype, DI.
> Keep in mind that these patterns are framework-independent. They exist not only in extbase.

#### Singleton

Singletons are objects which only exists once at runtime. That means during creation of an object, extbase checks if an object of the same type already exists. If so, it is returned. Otherwise a new object is instantiated.
> I wonder about the difference concepts of oop here: there are classes, which purely exist to create similar objects of the class. Then again there are static classes which, to me, sound like what singletons are supposed to solve. The difference is that in the first case no object is created. Maybe this is the whole difference. 

In extbase, you use the methode `makeInstance()` of the class GeneralUtility to instantiate objects. This method checks for existing objects of the requested type. The `new()` method is PHP native.

#### Prototype
The opposite of a singleton: when objects are requested/created extbase always creates a new object.

#### Dependency Injection (DI)
The goal is to get rid of the load of the object connections to its environment (dependencies). This is done by inversion of control.
The connections are only relevant to load the dependencies, not the purpose of the object.

Practical example of DI in extbase: using a Repository in a Controller. Instead of instantiating a Repository object using `new()` you just tell the controller the class you wish and the framework does the rest for you (that is, searching an instance and returning it to the controller).

In extbase (!) there are two kinds of DI: Constructor DI and Setter DI. Typically in TYPO3 Setter DI is the way to go and looks like this:
```php
/**
  * Blog Repository
  *
  * @var \ExtbaseBook\Simpleblog\Domain\Repository\BlogRepository
  */
protected $blogRepository;

public function injectBlogRepository(\ExtbaseBook\Simpleblog\Domain\Repository\BlogRepository $blogRepository)
  {
    $this->blogRepository = $blogRepository;
  }
```

Constructor DI looks pretty similar: instead of creating a new method, the constructor method is used:
```php
/**
  * Blog Repository
  *
  * @var \ExtbaseBook\Simpleblog\Domain\Repository\BlogRepository
  */
protected $blogRepository;

public function __construct(\ExtbaseBook\Simpleblog\Domain\Repository\BlogRepository $blogRepository)
  {
    $this->blogRepository = $blogRepository;
  }
```

## Domain-Drive Design (DDD)

The whole business process and logic of the customer is called a "domain". DDD is used to put the focus on this domain and neglect technical specifications, such as infrastructure or programming language.
Extbase is based upon DDD, so it doesn't provide e.g. an Image upload function, but offers a quick way to implement the domain.

The application draft is primarily based on a model. A model is an abstraction of a real object. The domain model is a plan or blueprint of the containing objects, their properties and their relations.
The domain model is created by the customer (the domain expert) and the developer (either consultant or product manager). It is important to not enload the domain model building process with technical details. The domain model should be comprehensive to the customer without technical knowledge.

### Entity
