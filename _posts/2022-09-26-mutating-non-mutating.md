---
title: Mutating and Non-Mutating Methods
date: 2022-09-26
---

# [Part 2: Mutating and Non-Mutating Methods](https://launchschool.com/blog/mutating-and-non-mutating-methods)

Topics:
- Methods
- How can methods be mutating or non-mutating?
- Assignment vs. concatenation

## Mutating and Non-Mutating Methods

When discussing whether a method is mutating, be clear about what the method would be mutating:

> For example, the method `String#sub!` is mutating with respect to the String used to call it, but non-mutating with respect to its arguments.

## Non-Mutating Methods

A **non-mutating method** changes neither the object that called the  method nor the arguments passed into the method.

> All methods are non-mutating with respect to immutable objects.

- e.g., when we pass in an Integer, which is immutable, into a method, the method is non-mutating with respect to the Integer.

## Assignment is Non-Mutating

The assignment operator, `=`, acts like a non-mutating method because assignment only points a variable to a different object instead of changing the object referenced by the variable.

When this code runs, what values do `s` and `t` have?

```ruby
def fix(value)
  value.upcase!
  value.concat('!')
  value
end

s = 'hello'
t = fix(s)
```

We initialize local variable `s` to string `hello` and pass in that string to `fix` as an argument. At this point `s` and `fix` point to the same string. In the `fix` method, we invoke `upcase!` on the string referenced by `s` and `fix`. This string now has a value of `HELLO`. Then, we invoke `concat` on that string `HELLO` and pass in the string `!` as an argument. The string referenced by `s` and `fix` now has a value of `HELLO!`. Then, we return this string as the return value of `fix` and initialize local variable `t` to this return value, `HELLO!`. At this point, `s` and `t` both point to the string `HELLO!`.


What values do `s` and `t` have in this modified code example?

```ruby
def fix(value)
  value = value.upcase
  value.concat('!')
end

s = 'hello'
t = fix(s)
```

`s` will point to the string `hello` and `t` will point to the string `HELLO!`. Shortly after we pass in `s` and initialize the `value` variable to the object referenced by `s`, we reassign `value` to a new string object since `upcase` returns a new string. Conseqeuently, we can no longer access the object referenced by `s` in the `fix` method and `s` remains pointing to the string `hello`. `value` now points to a new string `HELLO`. Once we invoke the `concat` method on `value` with an argument of `!` we mutate this new string to have a value of `HELLO!`. Then, we return a reference to `HELLO!` and store that reference in `t`. Thus, `t` points to `HELLO!`.

> In this modified code, we assign the return value of `value.upcase` back to `value`. Unlike `#upcase!`, `#upcase` doesn't mutate the String referenced by `value`; instead, it creats a new copy of the String referenced by `value`, mutates the new copy, and then returns a reference to the copy. We then bind `value` to the returned reference.
>
> `s` and `t` now reference different objects, and the String referenced by `s` still references its original value. What happened?
>
> ... `value = value.upcase` bound the return value of `value.upcase` to `value`; `value` now references a different object than it did before. Prior to the assignment, `value` references a different object than it did before. Prior to the assignment, `value` referenced the same String as referenced by `s`, but after the assignment, `value` references a completely new String; the String referenced by `#upcase`'s return value.

![](https://miro.medium.com/max/1400/0*Mofi589HU0ji1eqr.png)


What if we modify the code again, what values do `s` and `t` have?

```ruby
def fix(value)
  value << 'xyz'
  value = value.upcase
  value.concat('!')
end

s = 'hello'
t = fix(s)
```

Before we invoked `<<`, `value` and `s` pointed to the string object `hello`. When we invoke `<<` on `value`, we mutate the value of the string referenced by `value` and `s` to `helloxyz`. We then assign `value` to the return value of `value.upcase`, which is a new string, `HELLO`. At this point, `value` and `s` point to different strings. Then, we return the return value of invoking `concat` on `value`, which is a reference to the string object, `HELLOXYZ!`. We initialize `t` to this string object. `s` points to `helloxyz` and `t` poits to `HELLOXYZ!`

## Mutating Methods

We describe methods as:
> mutating with respect to an argument or its caller if it muates its value in the process.

Consider `String#strip!`, which removes whitespaces from a string object:

```ruby
>> string = "  hi  "
=> "  hi  "

>> string.object_id
=> # a number

>> string.strip!
=> "hi"

>> string.object_id
=> # the same object id as before
```

`String#strip!` mutates its caller, `string`, so the object remains the same, but the value changes.

Most methods that mutate their caller use `!` at the end of the method name.

However, there are exceptions. Some methods mutate the caller, even though these methods don't use `!` at the end of their names, e.g.:
- `String#concat`
- `#[]=`
- `#<<`


## Indexed Assignment is Mutating

```ruby
name_string[0] = "M"
array[5] = Person.new
friend[:age] = 21
```

`#[]` mutates the object, e.g. `friend`.

What does this code output? Why?
```ruby
def fix(value)
  value[1] = 'x'
  value
end

s = 'abc'
t = fix(s)
p s
p t
p s.object_id == t.object_id
```

We initialize a local variable `s` to the string `abc`. Then, we pass in `s` as an argument when we invoke the `fix` method. At this point, `value` and `s` reference the same string. We invoke the `String#[]=` method on this string and pass in the Integer `1` and the String `x` as arguments. This invocation mutates the string referenced by `value` by replacing the content at index `1` of the string with `x`. Thus, the value of the string is now `axc`.


We return and initialize a new local variable `t` to this string, `axc`. At this point, `s` and `t` both point to to the same string, so we will output this string and `true`.

What will the object id be of this array and the relevant element before and after indexed assignment?

```ruby
numbers = [6, 7, 8]
p numbers.object_id
p numbers[1].object_id

numbers[1] = 9
p numbers.object_id
p numbers[1].object_id
```

The object id for `numbers` will remain the same, but `numbers[1]` will reference a different Integer. In other words, we mutated the Array `numbers` by reasssigning `numbers[1]` to a different Integer, but did not create a new Array.

## Concatenation is Mutating

The `#<<` (aka **shovel operator**) mutates the calling object by appending a value of this calling object instead of creating a new object. By contrast, the `+=` is non-mutating since this other method creates a new object.

What will this code output? Why?

```ruby
title = "Mr"
p title
p title.object_id

title << "s"
p title
p title.object_id
```

`p title` will output the String `Mr` before we invoke the `String#<<` and `Mrs` after we've invoked `#<<`. We will output the same object id before and after concatenation.

## Setters are Mutating

Setters are like indexed assignment because both methods:
1. mutate objects
2. use syntax like `something = value`

What is this code doing?
```ruby
person.name = 'Hercules'
person.father = 'Zeus'
```

We mutate the `person` object by assigning the `name` instance variable to `Hercules` and `father` instance variable to `Zeus`.

## Refining the Mental Model

Ruby must use pass by reference in mutating methods because passing objects in by value prevent methods from changing the original object.

Here are some guidelines for mutating methods:
- Most, but not all, mutating methods use `!` at the end of their names
- Setters and indexed assignment are mutating
- Regular assignment and assignment operators are non-mutating

## Conclusion

- Whether a method is mutating is dependent on the arguments passed in
- A method is mutating, with respect to its arguments, when the method changes the arguments
- A method is non-mutating when the method changes none of its arguments.
- Assignment is like a non-mutating method, example operators:
  - `=`
  - `+=`
  - `-=`
- Mutating operations and methods include:
  - Indexed assignment
  - Setter methods
  - `#<<` - the shovel operator used for concatenation
