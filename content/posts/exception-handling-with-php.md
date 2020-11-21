---
date: "2017-04-10T15:56:44+06:00"
title: "Exception Handling with PHP"
---

### What is Exception

Exception is an error condition which change the normal flow of code execution. Exceptions are catchable. That means, we can catch and try to recover or continue with the execution of the program.

**'errors' vs 'exceptions' :**
Generally errors occur at the language level (ie, the syntax is wrong, missing parenthesis etc)

### Exceptions in PHP

Exceptions were introduced in PHP 5. It is used in an object oriented way. The exception model of PHP is very similar to exception model of other programming languages.

Exceptions can be thrown and caught.

**one basic example,**

```php
  try {
    throw new Exception('An Exception');
  } catch (Exception $e) {
    echo $e->getMessage();
  }
  //output : An Exception
```

- **throw** : The thrown object must be an instance of the Exception class (or a subclass of Exception). Otherwise, there will be a PHP Fatal Error.
- **try** : If there is a 'try' block, then there must be atleast one 'catch' or 'finally' block. (Otherwise PHP Fatal Error)
- **catch** : When an exception is thrown, code following the statement will not be executed, and PHP will attempt to find the first matching catch block. If an exception is not caught (either by 'catch' or 'finally' block), there will be a PHP Fatal Error with an "Uncaught Exception ..." message (unless a handler has been defined with set_exception_handler method). Exceptions can also be thrown (or re-thrown) within a catch block. 
- **finally** : Introduces in PHP 5.5. 'finally' block can be used after or instead of catch blocks. Code within the finally block will ALWAYS be executed after the try and catch blocks ( regardless of whether an exception has been thrown or not)


#### Example,

```php
function inverse($number) {
  if ($number==0) {
      throw new Exception('Division by zero.');
  }

  return 1/$number;
}

try {
    $random_number = rand(0,5);
    $result = inverse($random_number);
    // ONLY echo when no exception is thrown
    echo $result;
} catch (Exception $e) {
    //ONLY echo if there is an exception
    echo "Exception Message :".$e->getMessage();
} finally {
    // always echo
    echo "I am always there";
}
```


> Note : Internal PHP functions mainly use Error reporting, only modern Object oriented extensions use exceptions. However, errors can be simply translated to exceptions with ErrorException. - [php.net](http://php.net/manual/en/language.exceptions.php)