---
title: Written Asssesment Notes - QAT Environment
date: 2022-08-26
---

THIS: The purpose of this entry is to focus on the principle of _shipping_ over perfection and getting feedback from my peers to identify where I can clarify concepts.

Dear Friends,

These notes will most definitely contain lots of errors. May I please have you review these notes and email me with your questions? e.g. Where you are confused/need clarification on? Or share your own mental models with me.

Thanks,

Richard

# Prep Notes

## Written Assessment Prep Checklist

- [ ] Be able to clearly explain:
  - [ ] local variable scope, especially how local variables interact with method invocations with blocks and method definitions
  - [ ] mutating vs. non-mutating methods, pass-by-reference vs. pass-by-value
  - [ ] Review the two lessons on these topics thoroughly:
    - [ ] working with collections (Array, Hash, String)
      - [ ] https://launchschool.com/lessons/85376b6d/assignments
    - [ ] popular collection methods (`each`, `map`, `select`, etc).
      - [ ] https://launchschool.com/lessons/c53f2250/assignments
  - [x] [variables as pointers](https://launchschool.com/books/ruby/read/more_stuff#variables_as_pointers)
  - [x] `puts` vs `return` [link](https://launchschool.com/books/ruby/read/methods#putsvsreturnthesequel)
  - [x] `false` vs `nil` and the idea of "**truthiness**"
  - [x] method definition and method invocation
  - [x] implicit return value of method invocations and blocks
  - [x] how the `Array#sort` method works

- [ ] Do initial pass through (rough attempt to explain each concept)
- [ ] Revisit each concept and check against sources.

### Method definition and method invocation

A method definition consists of the keyword `def` followed by the method name, optional parameter, optional body, and the `end` keyword. A method invocation involves an object calling the method and (optionally) passing in arguments.


### Implicit Return Value of Method Invocations and Blocks

Methods and block implicitly return the last evaluated expression in the given method or block, unless we use explicit `return`.

### `Array#sort`

- The `#sort` method implements the spaceship operator, `<=>` to compare and sort elements in a collection. By default, the `sort` method will order elements in non-descending order (least to greatest). If you pass in a block, you can change the ordering of the elements.

- `<=>` is a method that accepts two operands, the calling object and an argument, e.g. `1` and `2` in `1 <=> 2`. The spaceship operator returns one of 4 values when comparing operands:
  - `-1` When the calling object (left operand) is less than the right, e.g. `1 <=> 2`
  - `0`, when the calling object and right operand have the same value.e.g., `1<=>1`
  - `1`, when the calling object has a greater value than the right operand. `2<=>1`
  - `nil`, when the calling object and the right operand are of different data types and uncomparable, e.g. `31 <=> '12'`, we are unable to use the spaceship operator to compare a number with a string*. *unless you override the spaceship operator and redefine the operator.
- Is `Array#sort` mutating?
  - No. This `sort` method will return a _new_ array containing elements from the calling object that we've sorted according to the value of the block.



### `false` vs `nil` and the idea of **truthiness**

**Truthiness** is a quality that describes whether an object will evaluate to `true` or `false` in a boolean context.
- Variables that are **truthy** evaluate to `true` in a boolean context.
- Variables that are **falsy** evaluate to `false` in a boolean context.
- All values are truthy, except for `false` or `nil`.
- `false` and `nil` are `falsy`, i.e. these values evaluate to `false` in a boolean context.
- Truthy is not the same as `true`. For instance, the value `1` is truthy, but `1 == true` would evaluate to `false`.
- Falsy is not the same as `false`. For instance, `nil` is falsy, but `nil == false` would evaluate to `false` because `nil` and `false` are different objects.



### [variables as pointers](https://launchschool.com/books/ruby/read/more_stuff#variables_as_pointers)

- Variables store **pointers**, not values, to an **address spaces** in memory.

```ruby
a = "hi there"
b = a
a = "not there"
```

We reassign `a` to "not there". However, evaluating `b` will still return "hi there" because `b` contains a pointer to "hi there".

![](https://d2aw5xe2jldque.cloudfront.net/books/ruby/images/variables_pointers1.jpg)


```ruby
a = "hi"
b = a
a << ", Bob"
```

We _mutate_ the string referenced by `a`, which is also referenced by `b`. Therefore, evaluating `b` will return `hi, Bob`

![](https://d2aw5xe2jldque.cloudfront.net/books/ruby/images/variables_pointers2.jpg)

What's `a`, `b`, and `c`? What if the last line was `c = a.uniq!`?

```ruby
a = [1, 2, 3, 3]
b = a
c = a.uniq
```

`a` and `b` point to `[1,2,3,3]`. `c` points to `[1,2,3]`. If the last line was `c = a.uniq!`, then `a`, `b`, and `c` would point to `[1,2,3]`.

What is `a` after the `test` method returns? Did the method modify the value of `a`?

```ruby
def test(b)
  b.map {|letter| "I like the letter: #{letter}"}
end

a = ['a', 'b', 'c']
test(a)
```

> When we use variables to pass arguments to a method, we're essentially assigning the value of the original variable (a in this case) to a variable inside the method (b). This is equivalent to executing b = a. Inside the method, the operations we perform on the b variable determine whether the value of a will change. Some operations, like map, will have no affect on a. Others, like map! will mutate the value assigned to a.


### `puts` vs `return` [link](https://launchschool.com/books/ruby/read/methods#putsvsreturnthesequel)

> Ruby methods ALWAYS return the evaluated result of the last line of the expression unless an explicit return comes before it.

```ruby
def add_three(number)
  number + 3
end

returned_value = add_three(4)
puts returned_value
```

We initialize the `returned_value` variable to the value returned by the `add_three` method. Then, we print the `returned_value`, `7`, to the output.

What happens when we add an explicit `return` to this code?

```ruby
def add_three(number)
  return number + 3
  number + 4
end

returned_value = add_three(4)
puts returned_value
```

We output `7` because we return the value of `number + 3` out of the `add_three` method using the `return` keyword. We don't execute `number + 4`.

## Snippets/Notes on the Written Assessment Preparation Process

### [Zelinksi](https://medium.com/@bziggz/advice-on-the-practical-aspects-of-rb109-written-assessment-1f86c3ca0c81)

Pre-write questions to study guide and study group questions.

- [ ] Make a checklist for test day:
  - Set one time for 2 hour 40 min for reviewing/wrapping up.
  - Set a strategic 70 min timer for assessing progress --> to speed up if needed.
  - Write down the ansewrs to questions in your markdown app.
  - Review first three questions.

### [Callie Buruchara](https://medium.com/launch-school/passing-launch-schools-first-assessments-rb109-4b2b047060dc)
- Strategies:
  - Be as concise as possible in answering questions (more time to review/add later).
  - <https://medium.com/launch-school/managing-anxiety-in-launch-school-assessments-c8464b5d2e3d>
  - "Is there any aspect of the question that I failed to answer, either because my response is incomplete or off-track?"

### [Felicia](https://www.youtube.com/watch?v=NS1ar08blQk)

1. **First pass**: Get a general overview and sense of what's in the course and where you need to brush up on.
   1. Go slow.
   2. No notes.
   3. Do the exercises.
   4. Follow along with the code.
   5. Take the quiz.
   6. Repeat for every single lesson in course.

2. Second pass: Concise notes to capture core concepts.

3. Third (or greater) Pass: Assessment prep mode and creating your own study guide.
   1. Go back to all lessons.
   2. Take notes on important concepts for the assessment.
   3. Review quizzes.
      1. Hide answers.
      2. Attempt to answer all (or almost all) questions correctly.
      3. If successful, you're ready to move on to next lesson.
   4. You're probably ready for the assessment now.

Study Guide:

- Copy the topics from study guide into new notes.
- Put examples under each of the topic headers/sub-headers.
  - ![Study Guide](images/2022-08-16-07-48-41.png)
- When done, put "DONE" next to header.
  - ![Study Guide](images/2022-08-16-07-48-13.png)
- Quick review.

Note-taking process:

1. Quick bullet point process of core concepts.
2. Summarize and recall key concepts on own words while providing examples for all of them. Explain what the code demonstrates, precisely.

Benefits of the FB approach:

- Minimize time being stuck on concepts
- Just come back to the material later on.

## [Srdan](https://medium.com/how-i-started-learning-coding-from-scratch/advices-for-109-written-assessment-part-1-6f7fa821cf84)

### Part-1:
Non-technical:

- Use markdown:
  - backticks, single tick for code on one line (``` ` ```).
    - e.g. `dog.bite!(bad_boy)`
- Use paragraphs for flow/communication. The harder it is to grade you, the more likely you are to lose points.
- Make sure you know what each question is looking for and give the question what it's asking, precisely and concisely.

### Part-2:

#### Learn to use programming terms

```rb
1 a = 'hello'
2 b = a
3 a = 'goodbye'
```

##### My attempt:
On line 1, we initialize local variable `a` to the string `'hello'`. On line 2, we initialize variable `b` to the same string referenced by `a`. On line 3, we re-assign `a` to `'goodbye'`.

##### Srdjan's solution:
> On `line 1` of this code, local variable `a` is **initialized**.

- Remember **initialize**. You _initialize_ a variable when you assign a value to that variable for the first time.

> On `line 1`, you are initializing local variable `a` and on `line 2`, you are initializing local variable `b`.

- Remember **assign** and **reference**.

> On `line 1` you are **assigning** the string object with a value `hello` to the local variable `a` (remember that objects are just physical spaces in memory and local variables are referencing them ... local variable `a` is refering that string object with the value name.
>
> We are initializing a local variable `a` to a string object, and now this local variable references this string object.

- Remember **reassignment**.

On line 3, we aren't initializing `a` because we already initialized `a` on line 1. Instead, we are _reassigning_ `a` to reference a "different string object with a different value `goodbye`".

> On `line 1` of this code we are initializing the local variable `a` to a string object with value `hello` to it.
> On `line 2` we are initializing the local variable `b` to a string object that the local variable `a` is referencing. Currently, both of these local variables are pointing to the same object.
> On `line 3` we are reassigning the local variable `a` to a different string object with value `goodbye` so now, the local variable `a` is pointing to one string object with value `goodbye` and the local variable `b` is pointing to a string object with value `hello`.

A different example...

```ruby
def example(str)
  i = 3
  loop do
    puts str
    i -= 1
    break if i == 0
  end
end
example('hello')
```

<script src="https://gist.github.com/richardtvu/c129b2df688efabf98990814c6bf3962.js"></script>

#### My-Attempt:
On line 10, we invoke the `example` method and pass in a string `hello`. On line 1, we assign the variable `str` to the string we passed into `example`. On line 2, we initialize local variable `i` to Integer `3`. On lines 3-7, we invoke the `loop` method and pass in a block, which is defined as the `do..end` following a method invocation. On each iteration of the `loop`, we invoke the `puts` method and pass in `str`, which outputs `hello`. Then, we re-assign `i` to `i-1`. Once `i == 0` evaluates to `true`, we break out of the loop with the `break` keyword.

This example demonstrates the concept of variable scope, in particular the need to pass a variable into a method to use the variable within the method as well as concept of inner scope. A block creates an inner scope, from which we can use local variables defined outside of the block in the block's outer scope.

#### Srdjan's explanation

> On `lines 1-8` we are defining the method `example` which takes 1 parameter. On `line 10` we are calling the method `example` and passing in the string `hello` as an argument to it. And here is the first thing which confuses a lot of people. and (sic) it's important to distinguish...Methods are defined with parameters, but they are called with arguments.
>
> On `line 2` of this code we are initializing the local variable `i` and assigning it an integer with value `3`.
>
> On `line 3` we are calling the method `loop` (yes, loop is actually a method of the `Kernel` module) and **passing in** the `do..end` block as an argument. So the block here is passed to a method call as an argument.
>
> And also on `line 4` we are actually calling the method `puts` and passing in local variable `str` to it as an argument. **You are going to use a lot of passing in as an argument on the test. Get used to that phrase** (emphasis mine).
>
> On `line 5` the local variable `i` is reassigned. `-=` is actually reassignment and it is Ruby's syntactical sugar for `i = i - 1`. And while we are talking about syntactical sugars, that code is also one, since  is not an operator but a method and that code can also be written as `i = i.-(1)`. So inside of this code we are actually, reassigning the local variable `i` to the return value of a method call `Integer #-` on a local variable `i` with integer `1` passed to it as an argument.
>
> On `line 6` we are breaking out of the loop by using the keyword `break` if the value of the object that local variable `i` is referencing is equal to 0.
>
> On `line 10` we are calling the method `example` and passing in string `hello` as an argument.
>
> Finally, but not less important, this code **outputs** string `hello` 3 times and **returns** `nil`.That is very important to distinguish.The last evaluated expression is returned since we don't have an explicit `return` inside of the method definition. That last evaluated expression is `break if i == 0` in this case, which returns `nil`.

### Variable scoping

> Without running the code try to answer what will this code example output :

<script src="https://gist.github.com/richardtvu/34477477c4f12a667cadad680bd2bcf5.js"></script>

#### My Attempt
We initialize local variable `a` to integer `4` on line 1. On line 3-7, we invoke the `loop` method and pass in a `do..end` block. Within the inner scope of the block, we reassign `a` to integer `5` and initialize variable `b` to `3`. Then, we use the `break` keyword to exit the loop. On line 9, we invoke the `puts` method and pass in `a` as an argument. Since we reassigned `a` to `5` on line 4, this method invocation will output `5`. This output demonstrates the concept of variable scoping, in particular, variables defined from outside of the scope of a block can be accessed from within the block. On line 10, we invoke the `puts` method and pass in `b`, which raises an exception saying that we didn't define/initialize(???) the local variable. This exception illustrates the concept that variables defined within an inner scope, e.g. within a block, may not be accessed from without the block.

#### Srdjan's Solution

> The code outputs `5` and raises an error, undefined local variable or method `b`.
> we have two scopes. An inner scope which is defined by the `do..end` block and outer scope which includes everything else... **local variables that are initialized in an inner scope CAN'T be accessed in the outer scope, but local variables that are initialized in the outer scope CAN be accessed in an inner scope.
> This is why we can reassign the local variable `a` on line 4, but if we try to initialize the variable `b` it is not accessible in the outer scope. Can you find a way to make this code output the value of the local variable `b`?

To make the code output the value of the local variable `b`, simply initialize `b` outside the block.

### Example 2

<script src="https://gist.github.com/SrdjanCoric/e08a4ed0fb66ac4f50a60eef2c4cda60.js"></script>

#### My Attempt
We initialize local variables `a` to `4` on line 1 and `b` to `2` on line 2. On line `5` we initialize `c` to 3 and then reassign `a` to the same value as `c`. Therefore, the code will output `3` and `2` and return `nil`.

Areas of Improvement:
- Mention the `loop` method and passing in the `do..end` block to the `loop` method as an argument.
- Mention outer scope is where we initialized `a`.
- We can reassign `a` to the same object as `c` because we reassigned `a` in the same scope as `c`.
- Mention we are invoking the `puts` method and passing in a local variable `a` as an argument. Since `a` points to 3,`puts` outputs `3`.
#### Srdjan's Solution

> This code outputs `3` and `2`.

> On `line 1` we are initializing a local variable `a` with in outer scope.
> On `line 4` we call the `loop` method and pass the `do..end` block to it as an argument. Inside of this block we initialize new local variable `c` which has this block as its scope.
> On `line 6` we reassign the local variable `a` so that it points now to the same object that the local variable `c` is referencing. Since we are still in the inner scope defined by the block, local variable `c` is accessible.
> On `line 10` we call the `puts` method and pass the local variable `a` as an argument and this code outputs the value of variable `a` which is now `3` since we reassigned it inside of the block.
> What would happen if on `line 12` we added `puts c`? It would return an error of course just like in the previous example, since this variable is not available in the outer scope.


#### Redo Solution

On lines 1-2, we initialize local variables `a` to `4` and `b` to `2` in the outer scope. On lines 4-7, we invoke the `loop` method and pass in a `do..end` block as an argument. Within the block on line `5`,we initialize a local variable `c` to `3`. On line 6, we reassign `a` to the same object referenced by `c`. This reassignment is possible because we initialized `c` in the same scope that we access `c`.

Thus, `a` now points to `3` when we invoke the `puts` method and pass in `a` as an argument on line 10. Thus, our `puts` invocation outputs `3`. On line 11, we invoke the `puts` method and pass in `b` as an argument.`b` points to `2`, so `puts` outputs `2`.

### [Part 3](https://medium.com/how-i-started-learning-coding-from-scratch/advice-for-109-written-assessment-part-3-d39dceb06c0c)

#### Variable Shadowing

<script src="https://gist.github.com/SrdjanCoric/4c5852bcb96a3891032c55852e6bb920.js"></script>

##### My Attempt
We initialize local variables `a` to `4` and `b` to `2` on lines 1-2. On lines 4-7, we invoke the `times` method on `2` and pass in a `do..end` block with a parameter `a`. Thus, on line `4` the block variable `a` will shadow the local variable `a` defined in the outer scope, preventing us from accessing the outer scope `a` from within the block. Consequently, when we reassign `a` on line 5 to `5`, we're really re-assigning the block variable `a` and not the `a` we defined in the outer scope. When we invoke `puts` and pass in `a` as an argument on line 6, we will output `5`. We pass the numbers `0` and `1` to the block on 2 separate iterations. Since we iterate twice, we invoke `puts` twice and output `5` twice.

On line 9, we invoke `puts` and pass in the outer scope variable `a`, which points to `4`. Thus, this `puts` invocation outputs `4` . Finally, when we invoke `puts` and pass in `b` as an arugment on line 10. This invocation outputs the value referenced by `b`: `2`.

Areas of Improvement:
- Specify the data type of `2` (i.e. integer `2`).
- On line `4`, we invoke the `times` method on integer `2` and pass in the `do..end` block. This `do..end` block has one parameter, `a`.

##### Srdjan's Solution

> This code outputs `5`, `5`, `4`, and `2` in this order.
> ....
> ....
> On line `4` we are calling the `times` method on integer `2` and passing in the `do..end` block as argument iwth one parameter `a`.
> ... on `line 5`? ... \[**variable shadowing** (vs) \]happens when parameter name of the block is the same as the name of the localv ariable was initialized outside of the block. ... \[vs\] prevents accessto variables of the same name initialized outside of the block.So on `line 5` we are actually assigninginteger `5` to the localv ariable `a` passed in as a parameter of te `do..end` block and the value of the localv ariable `a` inialized in outer scope remains `4`.


To fix this issue, rename the parameter `a` to another variable name, e.g. `some_var`.

### `Each`, `Map`, and `Select` Methods

- [x] Watch https://launchschool.medium.com/live-session-beginning-ruby-part-3-61180782f721


#### What do `Array#each`, `Array#map`, and `Array#select` methods do?

`[1,2,3,4].each {|num| puts num}`

#### My attempt

`each` iterates through each element in `[1,2,3,4]` and passes each element into the block as `num`. Then, we invoke `puts` and pass in `num` as an argument, which outputs the value of the `num`. Finally, `each` returns the original collection.

#### Srdjan's Solution

> [`each`] iterates through the array object passing each element of the array to the block, runs the block (in this outputting value of parameter num) and when it finishes every iteration it returns the original array. So, `each` method doesn't care about return value of the block.

#### What does `Array#map` do?

`[1,2,3,4].map {|num| puts num}`

#### My Attempt

`map` iterates through the array object, passing each element of the array to the block, runs the block (outputting the value of parameter `num`). When `map` finishes iterating, `map` returns a new array with elements from the original array transformed based on the return value of the block.

#### Srdjan's Solution

> iterates through ... [same] ...`Map` method actually takes return value of the block and moves it into a new array and when it finishes every iteration it returns that new array with elements which were passed in it (reteurn values of block of each iteration).

What is the return value of the block after each iteration?
-`nil` because `puts` always returns `nil`.

> ... so our example above would return a new array `[nil, nil, nil, nil]`. It would output all of this values from the original.

#### Rewording Srdjan's Solution

`map` iterates through the array object, passing each element of the array to the block and runs the block. On each iteration, `map` outputs the value of parameter `num` and moves the return value of the block to a new array. `map` returns this new array once `map` finishes iterating.

#### What does `Array#select` do?

`[1,2,3,4].select { |num| puts num }`

#### My attempt

`select` iterates over the array `[1,2,3,4]`, passing each element into the block and runs the block. On each iteration, `select` outputs the value of the parameter `num` and adds current element to a new array if the return value of the block is truthy. When there are no more to elements to iterate over, `select` returns this new array.

#### Srdjan's Solution

> What `select`  does differently now is, it considers the return value of the block **evaluates** to `true` or not and if it does it takes that element and puts it in new array. You can see that I have made word evaluate bold and that's because this word is very important. Everything in Ruby evaluates to boolean `true` except `false` and `nil`.

```rb
if 3
  puts "I evaluate to true"
else
  puts "I evaluate to false?"
end
```

`3` is not equal to `true`, but we will output `I evaluate to true` because `3` _evaluates_ to `true` in a boolean context. `3` evaluates to true because all values besides `false` and `nil` evaluate to `true` in a boolean context.


### [Part 4](https://medium.com/how-i-started-learning-coding-from-scratch/advice-for-109-written-assessment-part-4-e205174ece7b)

#### Mutating/Non-Mutating Ruby Methods

What are **mutating** methods in Ruby?
- Mutating methods change either the calling object or the arguments passed into the method.

Srdjan's Definition:
> ... methods which are changing the value of a calling object.

#### What is happening in this example?

<script src="https://gist.github.com/SrdjanCoric/231c776099ff292d528b2fc5c54e8e96.js"></script>

Invoking `object_id` on the string referenced by `a` returns the same value because `upcase!` is a mutating method. When we invoked `upcase!` on the string object referenced by `a`, `upcase!` change the value of the string object instead of creating a new string object. Thus, `upcase!` mutated the value of the calling object.

#### Srdjan's Explanation

> On `line 6` we are calling method `String#upcase!` on the object variable `a` is pointing to... This method is mutating method which means it is changing value of the object that is calling it, so the object stays the same.
> ... `line 9` we can see that the object hasn't changed see it still has the same object_id.


#### Answer the three questions in this example

<script src="https://gist.github.com/SrdjanCoric/a707892748950aed9d5f383461c3d86f.js"></script>

#### My attempt

Are these three local variables pointing to the same object?
- No. On lines 1-3, we initialize local variables `a`, `b`, and `c` to different string objects that have the same value. Thus, lines `7-9` will output different `object_id` values.

What about now?
- Yes. On lines 13-14, we reassign `a` to the same string referenced by `c`. We reassign `b` to the same string referenced by `a`. Thus, `a`, `b`, and `c` all point to the same string. Consequently, on lines 16-18, we will output the same value for each invocation of `puts`.

And now?
- No. On line 21-23, we reassign `a`, `b`, and `c` to the immutable Integer `5`. Because `5` is immutable, `a`, `b`, and `c` all point to the same integer object. Thus, we output the same value for each invocation of `puts` on lines 25-27.

#### Good. What about symbols?

<script src="https://gist.github.com/SrdjanCoric/a75112d8e682373acbfc80b9ecb31668.js"></script>

Symbols are also immutable, so lines 5-7 would all output the same value because local variables `a`, `b`, and `c` all point to the same object.

#### `+=` operator?

<script src="https://gist.github.com/SrdjanCoric/b531c6ec61c8a44a1a9385f7ed8cfb19.js"></script>

The `puts` invocation on line 3 will output a different value from the `puts` invocation on line 7 because `+=` is a re-assigns `a` to a new object instead of mutating the object referenced by `a`. That is, on line 5, we are reassigning `a` to a new string object with the value `hello world`.


## [Raul](https://medium.com/@raul.dehevia/launch-schools-109-written-assessment-a-non-native-english-speaker-s-perspective-d320b47368ba)

- Take notes on technical language instructor uses at study essions.
- Memorize the technical vocabulary.
- Start with being thorough in your answer.
- Then, pare down your answer to the essentials.
  - Identify what is important for each question.
  - Identify what you don't need to explain, in detail or at all.
- Make your own examples for the topics on the study guide.
- Goal: Have a template answer for each topic.
- Rinse and repeat with timer and compare & contrast your answer with template answer.

- Set 2 main timers: 2 h 40 min for review/wrapping up; 1 hr 10 min for half-way point to assess pace.
- Use stopwatch to control time for each answer.
- Limit time per question to 8 min and aim to spend as little time as possible on each question. Go back to hard questions after you've completed.
- Skim all questions in the beginning and assess:
  - Difficulty
  - The more time-consuming questions
- Review at end:
  - Typos
  - Format
  - Error Syntax/Logic
- Track answers on separate markdown.

## [Juliette](https://jsinibardy.com/preparing-launch-school-109-written-assessment)

- Make a list of exercises to re-do.
- Criteria for list:
  - Any small problem you didn't find a working solution to yourself.

- _Briefly_ read solution and re-attempt.
- Look up documentation for any new methods.
- Create flash cards for "important enough" information, i.e."
  - General knowledge/conceptual: regex, command line
  - Ruby's behavior: pass-by-value/reference/value-of-reference, scope, truthiness
  - Useful/foundational methods, e.g. `each`, `select`.

Attend study sessions.

- Make examples for each concept on study list.
- Pre-write template examples, e.g. "We initialized `variable_name` to `Object` `value`."

## [Callie](https://medium.com/launch-school/passing-launch-schools-first-assessments-rb109-4b2b047060dc)

- Pair up with study  buddy and send each other 3-4 small snippets of code with questions: Output? Return? Why? Concept illustrated?
- Time yourself and aim to answer each question in under 8 mins on average using markdown.
- Send code to each other and grade on LS standards (which are?)
- Pair code with students earlier in curriculum, e.g. Lesson 4 to get practice explaining concepts.

## Beginning Ruby Series

### [Prep Part 3](https://launchschool.com/blog/live-session-beginning-ruby-part-3)

Variables are pointing to an object. A variable can be initialized or (re)assigned to a new object or existing object.

Mental model: Variables point to objects.

"Everything is an object" refers to us being able to invoke methods on integers, strings, and other data types that we'd normally be unable to invoke methods on in different languages, e.g. java. In java, integers and strings are primitive types.

Data structure - a structure that holds data.
Collection - arrays/hashes/strings , a subset of data structures that hold data.

Symbols vs strings. `:a` vs `"a"`. Symbols are immutable, but strings are mutable in Ruby.

Arrays and hashes.

**Iterators** do this functionality:

```rb
loop do
  puts arr[idx]
  idx += 1
  break if idx == arr.size
end
```

`each`: Accepts a block and executes the chunk of code within the block _each_ element in a collection. Returns the original collection.

```ruby
arr.each do |n|
  puts n
end
```

What are blocks?
- "Anonymous functions" - Chris.
- Chunks of code we can pass into a method.

#### What are common mistakes when using `select` and `map` and the `Enumerable` module?

##### Imprecision with `select`

###### Take # 1, An insufficiently precise definition of `select`:

> `select` returns a new array that meets the criteria specified in the block.

###### Why is the above definition insufficiently precise?

The definition above will be sufficient for simple code, but fail in more complex code. For instance, this simple code will return the expected:

```rb
arr = [1,2,3]
odds = arr.select { |num| num.odd? }
p odds # => outputs and returns [1,3]
```

However, this code example would give a result that might be unintuitive:

```rb
arr = [1,2,3]
odds = arr.select {|num| num + 1 }
p odds # => outputs and returns [1,2,3]
```

What is the criteria specified in the block? There isn't a criteria and yet we return the entire collection. Wouldn't there be no elements selected if there is no criteria specified in the block?

And that's where the mistake in precision comes into play. Rather, `select` selects the elements in the collection for which the block returns a truthy value. `num + 1` is the last evaluated expression in the block and since every object/value besides `false` and `nil` are truthy,`select` will select _all_ elements in the collection.

###### Take #2: Another insufficient definition

> `select` returns a new array when the block evaluates to `true`.

```rb
arr = [1,2,3]
odds = arr.select {|num| num + 1 }
p odds # => outputs and returns [1,2,3]
```

This definition fits this example because the block evaluate to `true` ... but will fail in this slightly more complex example.

```rb
arr = [1,2,3]
odds = arr.select do |num|
  num + 1
  puts num
end
```

###### Memorize this `select` definition

> `select` returns a new array based on the block's return value. If the block's return value evaluates to `true`, then the element is selected.

This definition helps us answer the above example correctly:
`puts num` would return `nil`, so according to the definition #2, we don't return a new array. However, in reality, we do return a new array, the new array is an empty array, which is what definition #3 gives us.


`select` is a method we invoke on a collection. For a collection of size `n`, `select` accepts a block and returns a new array containing elements for which the block returned a truthy value. Therefore `select` will return an array whose size is between 0 and `n` elements.

##### `map`

Increment all numbers by 1 (transformation - new vs mutation):


###### New

```rb
# Manual
arr = [1,2,3]
new_arr = []
idx = 0
loop do
  new_arr << (arr[idx] + 1)
  idx += 1
  break if idx == arr.size
end
arr # => [1,2,3]
new_arr # => [2,3,4]

# `map`
new_arr = arr.map { |num | num + 1 }  # => [2,3,4]
```

###### Mutation

```rb
# Manual
arr = [1,2,3]
idx = 0
loop do
  arr[idx] += 1
  idx += 1
  break if idx == arr.size
end
arr # => [2,3,4]

# with `map!`
arr.map! {|num| num + 1}
arr # => [3,4,5]
```

##### Imprecision in `map`

###### Take #1

> `map` returns a new array based on the transformation specified in the block.

This definition works for transformation criteria like `num + 1`, but would fail to account for a criteria like `num > 1`.

```rb
arr = [1,2,3]
arr.map {|num| num > 1 } # => [false, true, true]
```
This example returns a new array with each element transformed into a booleans, e.g. `true` or `false`.

```rb
arr.map {|num| puts num } # => [nil, nil, nil]
```

###### Definition

> `map` returns a new array basd on the block's *return value*. Each element is transformed based on the return value.


#### Hashes

Modifying a hash in an array of hashes will also modify the array because what you're storing in the array is a pointer to the hash.


#### Main mistakes

1. Imprecise definitions (prevents understanding code examples more complex)
2. `enumerable` is mixed into arrays and hashes, e.g. `map`, `select`.




### [Assessment Prep Part 1](https://launchschool.com/blog/live-session-beginning-ruby)

- What is **syntactical sugar**?
- Where does the code come from?
- What is **variable scope**?

#### My attempt:

**Syntactical sugar** in Ruby is code that is shorthand for longer code. This syntactical sugar helps with making code more readable and concise. For instance, the `+=` operator is used to abbreviate `var = var + value` into `var += value`.

We can determine where code comes from... by ??? using `pry` or print statements?

**Variable scope** is where a variable can be accessed. Variables initialized in the outer scope of a block may be accessed from within the inner scope of the block. However, variables initialized within the inner scope of a block may not be accessed from without the block. Methods have their scope, i.e. only local variables passed into the method or initialized within the method may be accessed from within the method. Peer scopes do not conflict, i.e. variables declared in non-overlapping blocks won't be accessible to each other.


#### Notes

#### Syntactical Sugar

**Syntactical sugar**'s purpose is to help make Ruby "appear more expressive and english-like by hiding the fundamental or underlying mechanisms". Syntactical sugar hides the 'under the hood' implementation details. For example:

- An operator is actually a method call, e.g. `=` is actually a method. (I think????)
- `puts str` is unambiguous in that `str` could be a variable _or_ a method, like so

    ```rb
    # `str` as a variable
    str = 'hi'

    # `str` as a method
    def str
      "I'm a method"
    end

    puts str # When a method and a variable both have the same name, the variable takes precedence over the method in evaluation, e.g. this `puts` invocation will output "hi". To call #str specifically, use parentheses.
    ```
  - The ambiguity is syntactic sugar because not including the parentheses helps Ruby look more english-like.
- `puts str` is syntactic sugar for `puts(str)`, which is syntactical sugar for `puts(str())` if you're trying to invoke the method `str`. As you can see, `puts str` is a lot easier to read than `puts(str())`.

**Take-away**: Ruby hides programming details "under the hood" to make reading code more like reading English or help code appear more "expressive", as if the code were doing more with less. Regardless of what you think about syntactical sugar, it's important to understand what's happening under the hood.

Another example of syntactic sugar being used is in classes.
```rb
class Person
  attr_accessor :name
end

bob = Person.new
bob.name = 'bob'

p bob.name
```

At first glance, you might that the `name` in `bob.name` is a local variable.

```rb
# Syntactical sugar
bob.name = 'Bob'
# equivalent
bob.name=('Bob')
```

However, `name` is actually `Person#name=`, which is actually a method we invoke on the `Person` object refenced by `bob` and pass in the string `Bob` as an argument to `name=`. This example below represents how `name=` would be defined.

```rb
def name=(new_name)
end
```

#### What is the list of things that **Chris says "You must understand."?**

- Variables
  - different kinds of variables
  - variables as pointers
  - variable scope
  - variable initialization vs re-assignment
  - naming
- Methods
  - arguments
  - implicit return value
  - side effects
  - writing methods that are easy to invoke
  - naming
- Simple collection data structures
  - arrays, hashes, and strings
  - understanding of collection methods well
    - `select` and `map`
- Debugging
  - tinkering with puts
  - erase code to trap the error
  - pry
- Other
  - blocks
  - metaprogramming
  - ruby object model
  - testing
  - web development and frameworks


#### Where does the code come from?

- Core API
- Standard Library
- External Library, e.g. `pry` comes from pry gem.

Where did the `puts` method come from?

- `puts` comes from the `Kernel` module of the Core API.. **Core API** is the prebuilt code loaded into the Ruby runtime, so you can use some methods right out of the box instead of writing the methods yourself.

> `Kernel` - one of the most important moduels inside the Ruby language.

`Kernel` is loaded everywhere, so you can just call `puts` without the `Kernel.puts`.

The standard library is pre-written code that you load as needed, so that Ruby isn't bloated.

e.g. You can `require` the `prime` module to use a pre-built method for checking if a number is prime.

```ruby
p 1.prime? # => raises an error because we haven't required prime.
```

```ruby
require 'prime'
p 2.prime? # => true
```

An external library, e.g. `pry`.

Why know this?
- When working with frameworks like Rails, methods will seem to magically come from somewhere. The methods come from the core library, standard library, external libraries, classes, superclasses, etc.


# CONTINUE https://youtu.be/SYkDoRdJjCo?t=2197


#### Local variable scope

understand this to avoid unecessarily using globals or instance variables.



# [Ruby Notes](https://goalkicker.com/RubyBook/RubyNotesForProfessionals.pdf)

How do you talk about the operations that these operators do?
- `[]` - Bracket look up, is a method.
- `[]=` - bracket set - a method, mutating indexed assignment.

How are Bracket Lookup and Bracket Set methods defined?

```ruby
class Foo
  def [](x)
    puts "Looking up item #{x}"
  end
  def []=(x,y)
    puts "Setting item #{x} to #{y}"
  end
end
```

What are the assignment operators?

- simple assignment: `=`. initializes a new local variable or reassigns an existing variable.
- parallel assignment, e.g. `x, y = 3, 9`, used for swapping values.
- abbreviated assignment, e.g.`x +=y`, which is syntactic sugar for `x = x + y`

Local variables:
> can not be used outside the "declaration containers" scope

- Trying to use a local variable outside of the scope you declared the variable in will raise a `NameError: undefined local variable or method`

- If a local variable is defined in a method, the variable can be used only within the method. Same applies to blocks.

```ruby

def dragon_whisper
  whisper = "I love you, my dear."
  puts whisper
end

puts whisper #NameError
```

> [When you] declare a variable inside a `do..end` block ... curly braces `{}`, [the variable] will be local and scoped to the block it has been declared in.

```rb
dragon = "Amy"

loop do
  true_dragon_name = "Pocahontas"
  break
end

puts true_dragon_name
# NameError: undefined local variable or method `true_dragon_name'
```

- While you can't use local variables outside of its block, local variables defined outside the block can be used in the block.

```ruby
dragon = "Amy"

loop do
  puts dragon # Prints "Amy"
  break
end
```
- `if` and `case` statements don't have their own scope, so you can use variables declared within these statements in the **parent-scope** (the scope you wrote the statement in).

```ruby
if true
  friend = "Amy"
end

p friend
# "Amy"
# => "Amy"
```

- Local variables in the parent scope are accessible within blocks, but not to methods, unless you pass in the variables as arguments.

```ruby
love = true

def does_love_exist?
  love
end

puts does_love_exist? # NameError: undefined local variable or method `love'

def does_love_exist?(belief)
  belief
end

statement = "Love exists."

puts does_love_exist?(statement)
# "Love exists."
# => nil
```

- Block arguments will **shadow** variables defined outside the block: Any modifications to the block arguments won't affect the shadowed variable.

```ruby

friend = "Amy"

friends = ["JD", "Pocahontas", "Brian"]

def hug(person)
  person << " was hugged!"
  puts person
end

friends.each do |friend|
  hug(friend)
  puts friend # e.g. "JD was hugged"
end

puts friend
# "Amy"
# => nil
p friends
# ["JD was hugged!", "Pocahontas was hugged!", "Brian was hugged!"]
# => ["JD was hugged!", "Pocahontas was hugged!", "Brian was hugged!"]
```

How do you declare an array with default values?
-  Use `Array.new` and pass in a block that'll generate values for elements at each index.

```ruby
arr = Array.new 2, {"Boop"} # arr => ["Boop", "Boop"]
arr[1] = "Pooh" # arr => ["Boop", "Pooh"]
```

You can also set a default value for hashes in a similar way, so that when you mutate a key-value pair, you only affect one key-value pair.

```ruby
hash = Hash.new { "boop" }
hash[0] = "Hi"
hash[1] = "Yuppie"
hash # {0 => "Hi", 1 => "Yuppie"}
hash[2] # => "boop"
```

Falsy vs truthy?

```ruby
def check_truthy(var_name, var)
  is_truthy = var ? "truthy" : "falsy"
  puts "#{var_name} is #{is_truthy}"
end

check_truthy("false", false)
check_truthy("nil", nil)
check_truthy("0", 0)
check_truthy("empty string", "")
check_truthy("\\n", "\n")
check_truthy("empty array", [])
check_truthy("empty hash", {})
```

Outputs
```markdown
`false` is falsy
`nil` is falsy
`0` is truthy
empty `string` is truthy
\n is truthy
empty `array` is truthy
empty hash is truthy
```
