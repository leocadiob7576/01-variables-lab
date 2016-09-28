# Ruby Variables

## Objectives

1. Define a variable.
2. Create and reassign variables.
3. Define pass-by-value as it relates to variables.
4. Learn about the different types of variables in Ruby
5. Learn about the scoping of these variable types

## Variables in Ruby
Let's dive right in:

```ruby
first_number = 7
second_number = 14

sum = first_number + second_number

puts sum
```
The code above will print '21'.

```ruby
current_president = "Barack Obama"
puts "In 2016, the president was #{current_president}."
```
This code will print `In 2016, the president was Barack Obama.`.

> Note: The syntax of `#{current_president}` simply injects the value of the variable `current_president` into the string. This is called [string interpolation](http://stackoverflow.com/questions/10076579/string-concatenation-vs-interpolation-in-ruby) -- think of it as `"In 2016, the president was" + current_president` where you are adding that value to a string.

`first_number`, `second_number`, `sum`, and `current_president` are all **variables**.  Much like in math, variables are words or characters that hold values. In algebra, however, variables are only placeholders for numbers. In Ruby, a variable can point to almost any type of value including numbers, strings, arrays, and hashes.

## What is a Variable

As the examples above show, variables allow us to store information. We tell our computer to set aside some space to hold that information so we can retrieve it later. A variable is the location where the information resides, when we need it we know just where to look.

#### A Variable has a Name

```ruby
i
result
user1
brkfstCereal
all_words_in_the_dictionary
CountryOfOrigin
FIRST_NAME
age
longest_word
```
These would all be valid variable names in Ruby. They would not all be good variable names. There is strong convention among Rubyists to use what is known as *snake case* `this_is_an_example_of_snake_case` words are seperated by underscores.  This is opposed to *camel case*
`thisIsAnExampleOfCamelCase` where upcased characters indicate word breaks.

Variable names should start with a lowercase letter. A variable that begins with an uppercase letter is known as a **constant** and has some different behavior.

There are also some rules that mark invalid variable names:

```ruby
# X Invalid X
1st_place
end
danny's_age   
```

A Ruby variable cannot start with a number, be a Ruby reserved word, or have punctuation or space characters.

#### A Variable has a Value

A variable's name is like a label on a container. Its value is what is stored inside that container. The name points to the value. Above, `current_president` holds onto the value "Barack Obama" and `first_number` has the value of the number 7. As we will see, the value of a variable can change even when its name stays the same.

#### A Variable has a Type

A variable's type is the type of the value it holds. Ruby is what is known as a *dynamically typed* language. That means the value of a variable can change its type and does not need to be explicitly and permanently defined. There is nothing stopping you from changing the value of `sum`, which now is the number `21`, to the string `"whatever I want"`. 

It is also a *strongly typed* language. This means a variable will never be automatically *coerced* to another type without you explicitly changing the type. Adding two numbers will return a number, 2 + 2 returns 4; adding two strings will return a string, "2" + "2" returns "22"; adding a number and a string will raise an error, 2 + "2" raises a `TypeError`.

When you are building larger programs it is important to have in mind the type of the value that a variable refers to.

## Creating Variables

Variables are assigned values using `=` ("equal sign"), called the assignment operator.

```ruby
current_president = "Barack Obama"
puts "In 2016, the president was #{current_president}."
```

## Reassigning Variables

Now the variable `current_president` is equal to the string Barack Obama. Let's say somehow Stephen Colbert got elected as president in the 2016 election. To update `current_president`, you would just reassign the variable much in the same way that you first defined it:

```ruby
current_president = "Barack Obama"
puts "In 2016, the president was #{current_president}."

current_president = "Stephen Colbert"
puts "Now, it being the year 2017, the president is #{current_president}."
```
This will print out:  

```
In 2016, the president was Barack Obama.
Now, it being the year 2017, the president is Stephen Colbert.
```

## Bonus: 'Pass-By-Value'

We have seen that the variable itself, the location where information is stored, is distinct from the value stored at that location. Let's try something out to demonstrate this. We'll first declare a new variable with an original value, then do something to change that value, and finally we'll take a peek at our variable again.

```ruby
# Open up IRB and follow along
sound = "squeak"

# We can peek at the value of sound by typing its name
sound
# => "squeak"

sound.upcase
# => "SQUEAK"
```
Ok, the moment of suspense has arrived! Now if we type `sound` again what do you think its value will be?

...

...

```ruby
sound
# => "squeak"
```

Hmmm... `sound` is still pointing to the original lowercased value. What does this tell us? When `upcase` did its thing to the variable, what MUST `sound` have handed over to `upcase` for us to see this result?

Only it's *value*. In fact it must have made a *copy of that value* that `upcase` could operate on while still holding onto the original unaltered value. If this process did not happen the value 'squeak' wouldn't exist for us to look up and we'd only be able to see 'SQUEAK'.

This is what we mean by pass-by-value. A variable makes a copy of the value it holds and passes the copy over to something else that alters or changes it. The alternative process is known as pass-by-reference. Here, changes to a variable would alter what is stored in the actual location it refers to. After the process was complete the variable would be holding a new and different value.

## Variable Types

Variables hold data of any type in memory. In Ruby, there are a few different variable types we'll be going over. Note that here "type" does not mean "data type". Unlike in languages such as C, C++, and Objective-C, data types in Ruby do not need to be explicitly declared when variables are assigned.

We're going to focus here on three variable types. There are five total that are used in Ruby, but we will focus on the other two later when we learn about classes and object-orientation.

### Local Variables

You should already be familiar with declaring local variables. They're written most commonly as lowercase words. Most commonly, they look like this:

```ruby
languages = ["Ruby", "JavaScript", "C", "Python"]
```

Local variables are distinguished from other types of variables primarily by their "scope". Local variables have a "local scope", meaning that their definitions remain where they are declared.

If we define a variable within a method definition, only the method knows about that variable. Any type of reference to that local variable will result in an error;

```ruby
def my_method
  local_variable = "Only my method knows about me!"
end

puts local_variable
=> NameError: undefined local variable or method `local_variable' for main:Object
```

### Global Variables

Global variables, as you may have guessed, have a "global scope". These variables may be accessed anywhere in a program and are declared with a dollar sign in front of them, like so:

```ruby
$global_variable = "The whole program knows about me!"
```

Global variables should be used **very** sparingly, if at all. The concern with global variables is that because of their global reach, they can "break encapsulation" — if any method can modify a global variable, then any other place that relies on that variable can work in unpredictable ways. This can be very difficult to debug.

### Constants

Constants are written either in all UPPERCASE or they are Capitalized. They have a global scope when defined globally, and local scope when defined within classes and modules. Constants cannot be defined within methods. When constants are initialized, they should not be reassigned. Attempting to do so will result in a warning:

```ruby
CONSTANT = "I'm initialized!"
CONSTANT = "You shouldn't reassign me!"

=> warning: already initialized constant CONSTANT
```

You'll most often see constants used in class naming, or to hold data that will never need modification, like an array of words that will never be added to, or a hash of word definitions.

## Lab Instructions

You will assign a local variable named `greeting` that is equal to `"Hello World"`.

You should first make sure the test suite is running correctly by running `rspec`.

Upon the first run of the test suite you should see:

```
Failures:

  1) ./variable.rb defined a local variable called greeting and set it equal to 'Hello World'
     Failure/Error: greeting = get_variable_from_file('./variable.rb', "greeting")
     NameError:
       local variable `greeting' not defined in ./variable.rb.
     # ./spec/spec_helper.rb:14:in `rescue in get_variable_from_file'
     # ./spec/spec_helper.rb:11:in `get_variable_from_file'
     # ./spec/variable_spec.rb:5:in `block (2 levels) in <top (required)>'

Finished in 0.00075 seconds (files took 0.0839 seconds to load)
1 example, 1 failure
```

To solve this test failure, create a local variable `greeting` in the `variable.rb` file. Set `greeting` equal to the string `"Hello World"`. Run `rspec` to see if you did this correctly.


## Resources

- [ZetCode Ruby Variables](http://zetcode.com/lang/rubytutorial/variables/)
- [Wikibooks: Ruby Programming/Syntax/Variables and Constants](http://en.wikibooks.org/wiki/Ruby_Programming/Syntax/Variables_and_Constants)
- [Video review, f you need it](http://learn-co-videos.s3.amazonaws.com/ruby/about-variables-ruby.mp4)