---
layout: post
title:      "The Send Method: What it does and when to use it"
date:       2018-10-31 12:43:59 -0400
permalink:  the_send_method_what_it_does_and_when_to_use_send
---


First, let’s go over the need-to-know essentials. When you’re calling n method on an object using dot (.) notation, like in the example below, you’re essentially passing a message to it. 

```ruby 

“Paris, France”.downcase 
#=> “paris, france”

```

* The string is the **object**.
* The dot is the **method** in which we’re sending the object a message or command.
* Downcase or the argument is the **message**. 

We can also carry out the same command with the send method. 

```ruby

“Paris, France”.send(:downcase)
#=> “paris, france”

```

.send allows you to send a method call this way: 

send(:method_to_call)

When to use the send method:

Seeing it in an example might make it easier to comprehend when you should use it. 

In the Student Scraper lab in the OO Ruby section, we had to define an initialize method for our Student class that a) takes in an argument of a hash and b) uses “metaprogramming to assign the newly created student attributes and values in accordance with the key/value pairs of the hash”

``` ruby
def initialize(student_hash)
  student_hash.each do |attribute, value|
    self.send("#{attribute}=", value)
  end
  @@all << self
end

student_hash
=> {:name=>"Alex Patriquin", :location=>"New York, NY"}
@@all
=> [#<Student:0x00000003ad0270 @location="New York, NY", @name="Alex Patriquin">]
```

Here, the second method is essential taking attributes-and-value pairs in the existing student hash and churning out instance variable and value assignments. 

Send method uses in Ruby:
1. Allows you to assign attributes 
2. Allows you to call on methods by name with arguments
3. Allows you to call on methods without explicitly writing each individual method name every time 


**Sources:**
* I found [this article](https://blog.codeship.com/metaprogramming-in-ruby) on metaprogramming in ruby provided really helpful for understand what the send method/command does and when to use it. 
* Found [this video](https://www.youtube.com/watch?v=kNpcaaL_dZA) very helpful in really understanding the send method. 
* And this [forum](https://stackoverflow.com/questions/3337285/what-does-send-do-in-ruby) covers most of the send use cases


