---
layout: post
title:      "A Guide to Ruby *Yield* for When You Feel Kind of Lost "
date:       2018-11-08 17:42:19 -0500
permalink:  a_guide_to_ruby_yield_for_when_you_feel_kind_of_lost
---


For me, the most confusing part of learning and *actually* comprehending the concept of yield in Ruby is understanding when to use it. Before we go over common use cases of the ‘yield’ keyword, I’m going to attempt to explain what it is—mostly, as a refresher to myself. 

Important background:
- Blocks refer to code that lives between ‘do’ and ‘end’ keywords or curly braces { }, when we’re working with one liners. 

<hr>

<b>What does yield do?</b>
(Using examples from the Learn.co Yield and Blocks lesson).

```
def yielding
   puts “the program is executing the code inside the method”
   yield
   puts “now we are back in the method”
 end
 
yielding { puts “the method has yielded to the block! }

=> 
the program is executing the code inside the method
the method has yielded to the block!
now we are back in the method

```
Calling the yield keyword from within a method acts as a pause button that momentarily stops execution of the method you’re in, yielding the right of turn to the block, and returns to the method once the block runs. 

<hr>

<b>Yield with parameters</b>

Important background: 
- What is are parameters versus arguments? The term argument is commonly used to refer to variable names incorporated within a method definition and the value that’s passed in within a method call but there’s a distinction. 
- BUT there’s a distinction to be aware of: Parameter should refer to the variable in a method definition. While the argument is the data you pass into the method’s parameter(s).

The utility of yield lies in the ability to tweak a method to serve different purposes without having to rewrite it completely. (Think sandwich code!) Using yield allows you to “inject” an argument into a block. With yield + a parameter, you’re able to pass a value to the block you’re yielding to. Like so: 

```

def return_modified(array).  #our version of the collect method
   return_array = []
   array.each do |e|
   return_array << yield(e)
   end
   return_array
end

return_modified([1, 2, 3, 4]) do |x| 
  x * x
end
=> [1, 4, 9, 16]

```
       
We’re yielding to a block from inside another block. Note: This was a supreme point of confusion for me. Because in lessons on Learn.co, we were learning about yield in reference to a block but in labs, we were often writing methods that used yield—without seeing the block. I. did. not. get it. Here was the aha! moment for me: You pass in the block when you call the method. 

The return value for yield is the return value of the block that you’re yielding to. If the last line of code is simply an integer 8. The return value of yield would be 8. But here it’s [1, 4, 9, 16]. 

And that’s exactly how the #collect works. We’re yielding element to the block with #each but we’re capturing the return value of that block and returning it. 

<hr>

<b>Importance of yield</b>

Yield is essential in Ruby because it helps us avoid sandwich code—where the set up is the same, the body is different, and the tear down is different. Yield allows us to inject a value into a block—chunk of code—that helps our method function in a slightly different way. 


**Sources: **
https://www.codecademy.com/forum_questions/51c72e759c4e9d410501df42 
https://gist.github.com/lumberj/3768434

