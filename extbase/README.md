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


