# 1. In the code below, explain why the last line outputs 2.
 What's the underlying principle this example illustrates?
  ```
  str = 1 
  loop do 
    str = 2 
    break
  end 
  puts str
  ```

  On the line 4 of this code variable `str` is initialized and 
  and integer object with value 1 was assigned to it. On line 5, 
  `loop` method is called with a `do...end` block passed to it as argument, and inside this block variable `str` was reassigned to different object, that is to different integer with value 2. Finally on line 9 method `puts` is invoked and variable `str` was passed to it as argument.
  Method puts outputs the value of the variable `str` and returns nil.
  Underlying principle that his example illustrates is that local variables which are initialized in outer scope **can** be reassigned in inner scope defined by block. So, they can be accessed within the inner scope.
  7.5 mins

  2.Explain why the code below raises an exception.
  ```
  loop do
   str = 2
    break
  end 
  puts str
  ```
  The code raises an exception because the variable is initialized within the block which has it's own inner scope and local variables that are initialized inside the block **can't** be accessed outside of the block. So on line 21 we invoke method `loop` and pass it a `do..end` block as an argument and local variable `str` is initialized inside it therefor it is not available outside of the block.

  3. Suppose you can only see the code shown below, 
  and there are lots of code above the shown snippet.
   Can you say with certainty whether the below code snippet 
   will run? Why or why not? 
  ```
  # .. lots of code up here omitted 
  loop do
    str = 2
    break
  end
  puts str
  ```
  I can't say with certainty that this code will run or not. Problem is that variables that are initialized inside the block which has it's own inner scope can't be accessed outside of the block but we can't be sure that this variable wasn't initialized somewhere else in the code before the loop method invocation with a block passing as argument was omitted. So if somewhere above local variable `str` was initialized than this line 36 would be just reassignment and the code would work. But if it wasn't initialized than this line 36 would actually be initialization and code wouldn't work. 

  4. Explain why the following code raises an exception. 
  ```
  str = "hello"
  def a_method 
    puts str
  end 
  a_method
  ``` 
  This code raises an exception because we are initializing local variable `str` on line 45 and then we try to access it inside the method which starts below on line 46 and ends on line 48. Methods are self contained as far as scope of local variable is concerned so methods can't access local variables initialized outside of the method definition unless the variable was passed into the method as an argument along the method call. We are trying to call method puts and pass it local variable `str` as an argument but the method doesn't recognize local variable `str` since it was initialized outside of the method. So for example if we had similar method as the one above which takes 1 parameter like this `def a_method(str)`
  and we call that method on line 49 with an argument passed in `a_method(str)` and the argument is the local variable `str` initialized on line 45, then the code would work.

  5. Explain why the code below doesn't raise an exception,
   like it does in the previous example, and instead outputs "hello". What's the underlying principle in this code example? Why is there such a dramatic difference between the previous question and the code in this question? What's the relationship between the two str local variables -- are they the same variable, are they different, do they share the same scope? 
  ```
  str = "hello"
  def a_method 
    str = "world"
  end 
  a_method
  puts str
  ``` 
  This code doesn't raise exception because on line 57 we initialized local variable `str` and assign to it string object with value `hello`. Then on line 59 inside of the method definition we are initializing new variable which also has the name `str` and assigning to id string object with value `world`. This local variable has the same name is the one outside of the method but they are not actually the same local variables. They are 2 different variables with 2 different scopes pointing to 2 different objects. Variable initialized on line 57 is available in outer scope(outside of the method) so when we call method puts and pass it this local variable as an argument it will output string `hello` and return nil. We are calling method `a_method` on line 61 and it is returning execution of the last line of the method definition which in this case would be string object world but it is not outputting anything since we are not calling either methods puts, or print or p inside the method definition or outside of it we could pass our method call `a_method` as an argument to one of these methods I mentioned above (puts, print, p) and that way it would actually output string world.

  6. Explain why b is still "hello". 
  ```
  a = "hello"
  b = a
  a = "hi"
  a << " world"
   puts a
   puts b
   ```
   On line 68 we are initializing local variable `a` and assigning it string object `hello`. Then on line 69 we are initializing local variable `b` and assigning to it the same object to which local variable `a` points. At this moment we have 2 different local variables `a` and `b` pointing to the same object string `hello`. Then, on line 70 we are reassigning local variable `a` to different string object `hi`. Now, we have 2 different variables pointing at two different objects. We can think of the object as a physical space in memory. So local variable `a` is pointing to a string object `hi` which has it's own object id and local variable `b` points to different string object with different value `hello` and it has different object  id. On line 71 we are calling shovel method on local variable `a` and mutating object which this local variable points to so now local variable `a` reference the same string object as on line 70 but with different value `hi world`. So the object which local variable `b` wasn't change for these reasons so it still points to string object with value `hello`.

  7. How many variables and how many objects are there in the code below? How did you come up with your answer? 
  ```
  a = "hello" # 1 object
  b = "world" # 2 object 
  c = a # 2 object
  d = b # 2 object
  b = a # 2 object
  a = c # 2 object #
  ``` 
  On line 79 we are initializing local variable `a` and assigning to it string object with value `hello` . Currently there is 1 local variable and 1 object. On line 80 we are initializing another local variable `b` and assigning to it string object with value `world`.Currently there are 2 local variables and two different objects.
  On line 81, we are initializing local variable `c` and assigning to it the same object that local variable `a` is referencing. So now we have 3 local variables and 2 objects.
  On line 82 we are initializing local variable `d` and assigning to it the same object that local variable `b` is referencing so now we have 4 different local variables and still just 2 objects.
  Finally on line 82 we are reassigning local variable `a` but we are passing to it string object which local variable `c` is referencing which was basically the same object that local variable `a` was referencing before so it is reassigned to the same object so now we have still 4 different local variables with 2 different objects.

  8. Explain why the last line in the below code prints "hello". What does this demonstrate? 
  ```
  def change(param)
   param + " world"
  end 
  greeting = "hello"
  change(greeting) 
  puts greeting
  ``` 
  On line 96 we are initializing local variable greeting and assigning to it string  object with value `hello`. Then on line 97 we are calling method change and passing to it local variable greeting as argument. Finally inside the method definition on line 94 we are concatenating our string object that we passed as an argument to different string object with value `world` but since the #+ method is not mutating the caller we are actually creating new string object with value `hello world` and our argument object is left the same. Line 94 could be also written as `param.+(" world")`. So when we call method puts and pass it local variable `greeting` as an argument on line 98 local variable is not changed and method outputs `hello`.

  9.Explain why the last line in the below code prints "hello world". What does this demonstrate?
  ```
  def change(param)
    param << " world"
  end 
  greeting = "hello"
  change(greeting) 
  puts greeting
  ``` 
  On line 107 we are initializing local variable greeting and assigning to it string  object with value `hello`. Then on line 108 we are calling method change and passing to it local variable greeting as argument. Finally, inside the method definition we are calling method #<< on the string object that was passed in as argument. #<< method mutates the caller so the string object that was passed in as argument has changed its value now to `hello world`. This line 105 could have also been written as `param.<<(" world")`. So we are calling method #<< and passing to it a string ` world` as an argument but the method is mutating the caller so our string object that was passed in as argument and to what local variable greeting as pointing has now different value `hello world`. It is the same object though, with the same object id.
  On line 109 we are calling method puts passing it local variable `greeting` as an argument and it is outputting `hello world` for the reasons mentioned above.

  10. We're going to modify the change method slightly. Why does the last line print "hello" now? Why did adding the one extra line of code in change method so dramatically affect the final output? Be very precise with how you explain what's happening here. 
  ```
  def change(param)
   param = "hi" 
   param << " world"
  end 
  greeting = "hello"
  change(greeting) 
  puts greeting
  ```
  On line 120 we are initializing local variable greeting and assigning to it string  object with value `hello`. Then on line 121 we are calling method change and passing to it local variable greeting as argument. 
  Finally inside the method string object that local variable `greeting`  is pointing to is passed in as an argument so parameter `param` points to the same object. But, already on line 117 `param` is reassigned to a different string object with value `hi`. Now it is no longer pointing to the same object that local variable greeting is pointing to, so when mutate the calling object on line 118 by invoking method #<< on it is not the object that local variable `greeting` is pointing to but a different one so only the value of this new object is changed to `hi world` and our local variable `greeting` still references string object with value `hello`. 
  On line 122 we are calling method puts and passing to it as an argument local variable greeting which outputs `hello` for the reasons stated above.


  11. Explain why the last line outputs "hello". Be precise. 
  ```
  def change(param) 
    param += "greeting" 
    param << "hey" 
    param = "hi" 
    param << " world"
  end 
  greeting = "hello"
  change(greeting) 
  puts greeting
  ``` 
  On line 137 we are initializing local variable greeting and assigning to it string  object with value `hello`. Then on line 138 we are calling method change and passing to it local variable greeting as argument. 
  Finally inside the method string object that local variable `greeting`  is pointing to is passed in as an argument so parameter `param` points to the same object. But, already on line 132 `param` is reassigned to a different string object with value `hellogreeting`. += is actually syntactical sugar for reassignment and it could be also written `param = param + "greeting"` or `param = param.+("greeting") if we want to write it without any syntactical sugars since calling method #+ is also a form of syntactical sugar when it looks just like an operator without dot and parenthesis.
  From then on on lines 133-135 we are first mutating the object local variable `param` is pointing to but it is not the same object anymore as the one local variable `greeting` is pointing to. So neither this mutating call of shovel method and neither reassignment on line 134 and again call of method shovel on line 135 are changing the object local variable `greeting` is referencing. 
  So on line 139 when we call method puts and pass it local variable greeting as an argument it will output just `hello`. 
  12. Write down your definition of the Array#map method. Do not copy/paste from documentation; use your own words. 
  Method Array#map is called with a block passed in as an argument. It is returning a new array based on the blocks return value. Each element of the array is transformed based on the return value of the block. Just to point once again that if we call it without bang ('!') it won't mutate original array but it will create new one with the same number of elements as the original array where each element of new array will be the return value of the block during each iteration.
  13. Write down your definition of the Array#select method. Do not copy/paste from documentation; use your own words.
  Method Array#select is called with a block passed in as an argument. It is returning a new array based on the blocks return value. If the block evaluates to true then the element is selected and included in the new array.

  14. Explain why both of the code below return an array containing the same elements. Explain the subtle difference between the two lines of code. Which one is the preferred option and why? 
  ```
  [1, 2, 3].map {|n| n + 1}
  [1, 2, 3].map {|n| n += 1}
  ```
  These two codes return the array containing the same elements because when Array#map method is called on an object it returns new array with each element of the original array transformed based on the return value of the block. `n += 1` is actually a syntactical sugar for the reassignment `n = n + 1`. So both of these blocks return the same value. `n + 1` can be also written as `n.+(1)` and `n = n + 1` can be written as `n = n.+(1)` The first block is easier to read and understand so it is preferred choice over these two options.

  15. Some people don't fully understand the difference between map and select, and use map as they would select. However, they likely won't get the result they expected. Explain why the resulting arr is an array of booleans. 
  ```
  arr = [1, 2, 3].map do |n| 
    n > 2
  end 
  p arr
  ``` 
  Array#map is called with a block passed in as an argument. It is returning a new array based on the blocks return value. Each element of the array is transformed based on the return value of the block. Return value of each iteration of this block which was passed in as an argument to a map method call is a boolean value if the number passed to a parameter `n` is greater than 2 block will return true and if it smaller or equal to 2 it will return false. 

  16. The above code is a little odd, but perfectly valid Ruby. Suppose the person who wrote this code is trying to figure out why they're getting an array of booleans, so they put a puts in the block (see code below). Now, what did arr change into and why? Be precise with your explanation. 
  ```
  arr = [1, 2, 3].map do |n| 
    n > 2 
    puts n
  end 
  p arr
  ```
  Array#map is called with a block passed in as an argument. It is returning a new array based on the blocks return value. Each element of the array is transformed based on the return value of the block.
  When we call puts method on line 170 it is outputting the value of local variable `n` which is a parameter of the `do..end` block that was passed into the map method call as an argument. But method puts is always returning nil so return value of each iteration is actually nil now and so now we get new array which consists of arr.size number of nil. We could simply change this could to 
  ```
  arr = [1, 2, 3].map do |n| 
    puts n
    n > 2 
  end 
  p arr
  ```
  and it will then output the value of local variable `n` but the return value of the block won't be nil but the boolean true or false which is what we wanted.


  17. Continuing with the misunderstanding of map and select, suppose this person wrote the below code thinking that it should increment every element by 2. However, that's not how select works. What is arr and why? Be precise in your explanation and explain exactly how select works. 
  ```
  arr = [1, 2, 3].select do |n|
   n + 2
  end 
  p arr
  ``` 
  Array#select is called with a block passed in as an argument. It is returning a new array based on the blocks return value. If the block evaluates to true then the element is selected and included in the new array.
  `n + 2` is actually a method call String#+ and 2 is passed as an argument so it can be written like this `n.+(2)`. This code always evaluates to true since everything in Ruby evaluates to true except for false and nil. So we can say that everything in Ruby is truthy except for false and nil. 
  It is important to note that `n + 2` isn't true it **evaluates** to true. And select method includes element in new array if the return value of the block **evaluates** to true.

  18. Using the code above, let's say this person adds a puts in the block to try to figure out what's going on. What's arr and why? 
  ```
  arr = [1, 2, 3].select do |n|
   n + 2 
   puts n
  end 
  p arr
  ``` 
  The person is adding puts n on the last line of the block so as the method puts always returns nil, the return value of the block is nil so every iteration of the block will return nil and the result is going to be an empty array because none of the elements will be selected. 