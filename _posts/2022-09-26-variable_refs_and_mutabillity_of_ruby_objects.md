## [Part 1: Variable References and Mutability of Ruby Objects](https://launchschool.medium.com/variable-references-and-mutability-of-ruby-objects-4046bd5b6717)

Learning Objective:
- Learn about the context of how Ruby actually works
- Think about the questions of:
  - How Ruby manipulates variables and objects.
  - How are objects passed around in a Ruby program?

Expected Rewards:
- A deeper understanding of how Ruby works will help you:
  - Learn to predict what Ruby will do
  - When Ruby will do a behavior
  - Why Ruby does a behavior
- Which leads to:
  - Being a better programmer
  - Less bugs

### Topics of Part 1

- References - How do Ruby variables and objects connect to each other?
- How does mutability or immutabililty of objects relate to variable manipulation?

These topics serve as the foundation for better understanding mutating and non-mutating methods ... and pass-by-reference and pass-by-value in Ruby.

### Variables and References

**Objects** are data with a _value_, e.g. the Integer `1` has a value of 1.


### Variables _point_ to objects

We _initialize_ (or assign) variables to objects, e.g.

```ruby
>> greeting = "Hello"
=> "Hello"
```

We initialize a local variable `greeting` to a string object with the value `"Hello"`.

`greeting` _references_ (_points_) to the string object.

![`greeting` points to string object](https://miro.medium.com/max/1400/1*f4dcXlPkT6alWXk_-bVwJA.png)

When a variable **references** an object, that variable stores the object id of the object. You can access the value of the object by using the variable.

```ruby
>> greeting.object_id
=> 70101471431160 # The object id.

>> greeting
=> "Hello" # value of the string object
```

### If we change an object using one variable, we'll be able to see the change in the other variables referencing that object.

```ruby
>> farewell = "hello"
=> "hello"

>> greeting = farewell
=> "hello"

>> farewell.object_id
=> 70101471431160

>> greeting.object_id
=> 70101471431160
```

Both `farewell` and `greeting` point to the same string object.

![image of above statement](https://miro.medium.com/max/1400/1*Q4rI3BAIn3ydCEEi47vlfA.png)

Therefore, if we make a change to the object using one variable, we'll be able to see the change with the other variable.

```ruby
>> farewell.upcase!
=> "HELLO"

>> greeting
=> "HELLO"

>> farewell.object_id == greeting.object_id
=> true
```

### Reassignment points a variable to a new object, without changing the original object

```ruby
>> farewell = "good bye"
=> "good bye"

>> puts farewell
=> "good bye"

>> puts greeting
=> "HELLO"

>> greeting.object_id
=> 70101479528400

>> farewell.object_id
=> 70101471431160
```


When we reassign `farewell` to the string `"good bye"`, we make `farewell` point to a _different_ object than `greeting`. Thus, both variables will have different object ids and these objects, in this case, have different values.

![picture of reassignment results](https://miro.medium.com/max/1400/1*7sIvr2AHaWBA8yEBw8LTKw.png)

**Reassignment is non-mutating**.

### Mutability

**Mutability** of an object refers to whether you can change the value of an object.
- You _can_ change the value of a _mutable_ object.
- You _cannot_ change the value of an _immutable_ object.

### Immutable Objects

Numbers, `nil` and boolean objects are _immutable_ in Ruby, i.e. you cannot change the value of these objects.

```ruby
>> life_has_meaning = true
=> true

>> life_has_meaning = false
=> false
```

We initialize local variable `life_has_meaning` to the boolean `true`. When we reassign `life_has_meaning` to the boolean `false`, we are pointing `life_has_meaning` to a _different boolean object whose value is `false`.

```ruby
# Before reassignment. `life_has_meaning` points to the boolean `true`.
life_has_meaning --> boolean_object, value: true

life_has_meaning = false
# After reassignment
       [INACCESSIBLE] boolean_object, value: true
life_has_meaning --> boolean_object, value: false
```

We point `life_has_meaning` to a different object. The original boolean whose value is `true` is no longer accessible because we don't have any variables pointing to that object.


### Mutable Objects

You can change most objects in Ruby, i.e. you can mutate these objects.

Many objects have **setter methods** that let you change the value of these objects. Setters look like this: `someObject=`. For instance, Arrays have _array element setter_ methods, e.g. `Array#[]=`.

```ruby
>> friends = ["Joey", "Chandler", "Monica"]
>> friends[0] = "Rachel" # calls setter method
>> friends # => ["Rachel", "Chandler", "Monica"]
```

We invoke the `Array#[]=` (setter method) on the array referenced by `a` and pass in the index `0` as an argument to access the element at index `0`. We reassign this element to the string `"Rachel"`, which is a different string object than string `"Joey"`. Thus, we've mutated the `a` array since this array now contains a reference to a different string object than before.

Setters also show up in classes, e.g.:

```ruby
class Friend
  def name=(name_of_friend)
    @name = name_of_friend
  end
end

friend = Friend.new
friend.name = "Aaina" # Calls setter method for `name` attribute
```

You can use **index assignment** to change what an array element references, without making a new array:

```ruby
>> a = %w(a b c)
=> ["a", "b", "c"]

>> a.object_id
=> # some number

>> a[1] = '-' # Calls the `Array#[]=` setter method
=> "-"

>> a
=> ["a", "-", "c"]

>> a.object
=> # same obj id as last time.
```

![indexed assignment is mutating](https://miro.medium.com/max/1400/1*jt_mZVAoBt_yj7eVSVOMIg.png)

The object id for array referenced by `a` remains the same, but the element at index `1` now points to a different object, so we've mutated that array.

### A Brief Introduction to Object Passing

The main two ways we pass objects into methods are:
1. _pass by value_ - makes copies of the objects and passes in the copies. No mutation occurs here because we don't have access to the original objects.
2. _pass by reference_ - passes in pointers to where the objects are in memory. We can mutate mutable objects because we have access to the original objects.

### Developing A Mental Model

#### Ruby acts like pass by value when passing in immutable objects because we can't change those objects.

```ruby
def increment(a)
  a = a + 1
end

b = 3
puts increment(b) # prints 4
puts b            # prints 3
```

The integer `3` is an immutable object, so `b` will still point to `3` unless we reassign `b`. Thus, the `increment` method acts like pass-by-value because we don't change the value of the original object.

#### Ruby acts like pass by reference when passing in mutable objects

```ruby
def append(s)
  s << '*'
end

t = 'abc'
puts append(t) # prints abc*
puts t         # prints abc*
```

When we pass in `t` as an argument, we pass in the _reference_ to the string `abc`. That is, the local variable `s` within the method `append` points to the same string as `t`. Thus, when we invoke the `<<` method on that string, we will see our changes reflected in `t`. `t` still points to the same string, but the string now has a different value.


### Conclusion

- Ruby variables are names are objects.
- Variables _point_/reference objects in memory.
- Many variables can point to the same object.
- Changing an object referenced by many variables means all these variables will show the changes when these variables reference the object.
- Assignment is non-mutating.
- Some objects are **immutable**, i.e. can't be changed. e.g.,
  - numbers
  - booleans
  - `nil`
- You can change **mutable** objects.
- Rough mental model, Ruby _acts_ like:
  - **pass-by-value** for immutable objects
  - **pass-by-reference** for mutable objects










