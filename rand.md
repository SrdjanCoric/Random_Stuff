# 1. In the code below, explain why the last line outputs 2.
 What's the underlying principle this example illustrates?
  ```str = 1 
  loop do 
    str = 2 
    break
  end 
  puts str```

  2.Explain why the code below raises an exception.
  ```loop do
   str = 2
    break
  end 
  puts str```

  3. Suppose you can only see the code shown below, 
  and there are lots of code above the shown snippet.
   Can you say with certainty whether the below code snippet 
   will run? Why or why not? 
  ```# .. lots of code up here omitted 
  loop do
    str = 2
    break
  end
  puts str```

  4. Explain why the following code raises an exception. 
  ```str = "hello"
  def a_method 
    puts str
  end 
  a_method``` 

  5. Explain why the code below doesn't raise an exception,
   like it does in the previous example, and instead outputs "hello". What's the underlying principle in this code example? Why is there such a dramatic difference between the previous question and the code in this question? What's the relationship between the two str local variables -- are they the same variable, are they different, do they share the same scope? 
  ```str = "hello"
  def a_method 
    str = "world"
  end 
  a_method
  puts str``` 

  6. Explain why b is still "hello". 
  ```a = "hello"
  b = a
  a = "hi"
  a << " world"
   puts a
   puts b```

  7. How many variables and how many objects are there in the code below? How did you come up with your answer? 
  ```a = "hello" # 1 object
  b = "world" # 2 object 
  c = a # 2 object
  d = b # 2 object
  b = a # 2 object
  a = c # 2 object #``` 

  8. Explain why the last line in the below code prints "hello". What does this demonstrate? 
  ```def change(param)
   param + " world"
  end 
  greeting = "hello"
  change(greeting) 
  puts greeting``` 

  9.Explain why the last line in the below code prints "hello world". What does this demonstrate?
  ```def change(param)
    param << " world"
  end 
  greeting = "hello"
  change(greeting) 
  puts greeting``` 

  10. We're going to modify the change method slightly. Why does the last line print "hello" now? Why did adding the one extra line of code in change method so dramatically affect the final output? Be very precise with how you explain what's happening here. 
  ```def change(param)
   param = "hi" 
   param << " world"
  end 
  greeting = "hello"
  change(greeting) 
  puts greeting``` 

  11. Explain why the last line outputs "hello". Be precise. 
  ```def change(param) 
    param += "greeting" 
    param << "hey" 
    param = "hi" 
    param << " world"
  end 
  greeting = "hello"
  change(greeting) 
  puts greeting``` 

  12. Write down your definition of the Array#map method. Do not copy/paste from documentation; use your own words. 
  13. Write down your definition of the Array#select method. Do not copy/paste from documentation; use your own words.

  14. Explain why both of the code below return an array containing the same elements. Explain the subtle difference between the two lines of code. Which one is the preferred option and why? 
  `[1, 2, 3].map {|n| n + 1}` 
  `[1, 2, 3].map {|n| n += 1}`

  15. Some people don't fully understand the difference between map and select, and use map as they would select. However, they likely won't get the result they expected. Explain why the resulting arr is an array of booleans. 
  ```arr = [1, 2, 3].map do |n| 
    n > 2
  end 
  p arr``` 
  16. The above code is a little odd, but perfectly valid Ruby. Suppose the person who wrote this code is trying to figure out why they're getting an array of booleans, so they put a puts in the block (see code below). Now, what did arr change into and why? Be precise with your explanation. 
  ```arr = [1, 2, 3].map do |n| 
    n > 2 
    puts n
  end 
  p arr```

  17. Continuing with the misunderstanding of map and select, suppose this person wrote the below code thinking that it should increment every element by 2. However, that's not how select works. What is arr and why? Be precise in your explanation and explain exactly how select works. 
  ```arr = [1, 2, 3].select do |n|
   n + 2
  end 
  p arr``` 
  18. Using the code above, let's say this person adds a puts in the block to try to figure out what's going on. What's arr and why? 
  ```arr = [1, 2, 3].select do |n|
   n + 2 
   puts n
  end 
  p arr``` 