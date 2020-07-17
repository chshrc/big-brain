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


