# Functions and User Input

## Learning goals

- Learn how to make use of user input in shell scripts
- Learn how to use functions in shell scripts

## Introduction

In the last lesson, we went over the minimal basics of shell scripting. In this lesson, we're going to expand on it by introducing *user input* and *functions*.

## User input

What if we want the user of our script to input some information without needing to modify the script? In our examples above, we hardcode the value of our variables, for example:

```bash
name = "thomas"
```

What if instead, we want the caller of our script to be able to input what `name` is equal to? We can do this very easily using the `read` command. Here's what an example asking a user for a name and age looks like:

```bash
#!/bin/bash
echo "Please enter your name and age:"
read name age
echo "Hello $name! You are $age years of age."
```

This example reads in *two* variables, `name` and `age`, from user input. Someone calling our script would first get prompted to enter their name and age, after which they would be stored into their respective variables.

## Command substitution

**Command substitution** is just a fancy way to refer to using commands in our script. For instance, if we want to assign a variable the contents of a folder (using the `ls` command), we would use command substitution to do so. 

In order to substitute a command, all you need to do is wrap it with the `$()` syntax:

`files_in_directory = $(ls)`

That's it!

## Functions

**Functions** allow you to group code in such a way that lets you invoke them by name any number of times. They are useful for organizing and reusing code, and make your scripts modular and easier to maintain.

Defining a function is pretty straightforward; you can define them using the following syntax:

```bash
function_name() {
	# do something here
}
```

Let's say you want to make a function that greets a person and outputs their age:

```bash
greet() {
	echo "Hello, $1! You are $2 years old."
}
```

As you can see, the function name can be anything you want it to be. This name is what you use to invoke it later on. 

The `$1` and `$2` are its *arguments*, which allow you to pass in data every time you call it. You can use as many as you want (or none at all). 

> Note: While your scripts might still work with arbitrary levels of indentation, try to always indent once in every block to keep it readable. If you look at the line inside the `{}` brackets, you'll see that it is indented one level. You can do this using the `Tab` key. Keep a close eye on the indentation levels in all the example code shown to get a feel for it! 

In order to invoke the function, all you need to do is call it, with its arguments following it right after:

```bash
greet "Thomas" 24
```

That code would then output `Hello, Thomas! You are 24 years old.`

Keep in mind the function needs to be defined *before* you can use it, so make sure you don't define it later in your script. It's generally good practice to place all your functions at the beginning of your script, before any calls to those functions happen. It also has the added benefit of making it easier to understand the overall structure of the script when taking a glance at it.

## Sample script

Here's a sample script showing what the full script of the examples earlier could look like combined:

```bash
#!/bin/bash
greet() {
	echo "Hello, $1! You are $2 years old."
}

echo "Please enter your name and age:"
read name age
greet $name $age
```

## Conclusion

User input and functions are both powerful tools that make your bash scripts both interactive and modular. By leveraging user input, you can make your scripts flexible and adaptable to different situations. Functions, on the other hand, allow you to define and reuse groups of commands, making your scripts easier to read and maintain.