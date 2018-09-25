---
layout: post
title:      "Understanding object-oriented ruby relationships"
date:       2018-09-25 12:13:06 -0400
permalink:  understanding_object-oriented_ruby_relationships
---

As a beginner programmer, I had the hardest time wrapping my head around the concept (and formatting) of object-oriented relationships in code. It took weeks of reading explainers on blogs and watching OO Relationship tutorial videos. Here, I’m going to distill examples of belongs to, has many, and has many through relationships down to the nitty gritty, which helped me comprehend the concepts. Hopefully, it’s useful to you too. 

**Belongs to relationship**

The belongs to relationship means that ONE object (songs, dogs, etc.) has an owner (artist, shelter, pet owner, etc.). 

We’re able to show that in code by creating an attr_accessor for the owner. 

```ruby
class Dog
    attr_accessor :shelter
end
   
class Shelter
end

``` 

The above code allows us to create a new dog and assign ownership of the dog to a shelter. 

Step 1: Create new dog and assign it equal to “bandit” variable. 
Step 2: assign bandit’s ownership equal to shelter. 

```ruby
bandit = Dog.new    #step 1
bandit.shelter = Shelter.new      #step 2

bandit.shelter                 #reader method in account. This is telling you what shelter bandit belongs to.
=> #<Shelter:0x0000558f00ce56c8>

bandit    
=> #<Dog:0x00005634845bb8a0 @shelter=#<Shelter:0x00005634845bb878>>
``` 


``` 
