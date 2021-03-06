---
layout: post
title:      "Understanding object-oriented ruby relationships"
date:       2018-09-25 12:13:06 -0400
permalink:  understanding_object-oriented_ruby_relationships
---

As a beginner programming student, I had the hardest time wrapping my head around the concept (and formatting) of object-oriented relationships in code. But after a few weeks of reading explainers and watching OO Relationship tutorial videos, I can see OO relationships a little more clearly now. Here, I’m going to distill examples of belongs to, has many, and has many through relationships down to the nitty gritty, which helped me comprehend the concepts. Hopefully, it’s useful to you too. 

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

**Step 1:** Create new dog and assign it equal to “bandit” variable. <br>
**Step 2:** Create new shelter <br>
**Step 3:** Assign bandit's shelter attribute to your instance of Shelter that you just created <br>

Voila, Bandit is now a instance of the Dog class with a shelter attribute. 

```ruby

bandit = Dog.new #step 1
nycshelter = Shelter.new 
bandit.shelter = nycshelter #assigning the dog 

bandit.shelter
bandit
=> #<Dog:0x000055b18e671ca0 @shelter=#<Shelter:0x000055b18e671c78>>

``` 


But there's trouble in paradise. At this point, the instance of Shelter does not recognize or see the dog it owns. 

Here's how we know that:

```ruby
nycshelter.dogs
=> undefined method `dogs' for #<Shelter:0x00005557b6fca1f8>
(repl):15:in `<main>'   

```

When we ask nycshelter, an instance of Shelter, what dogs it has many of, it has no clue. Looking at the error, we have a clue, which points to what we need to do next. We need to define a method for dogs for the shelter. But every instance of shelter in general should probably know what dogs it has many of. 



**Has Many Relationships**

Here's the flip side of the belongs to relationship. A shelter *has many* dogs or you could say the shelter has a **collection** of dogs. 

To establish a has many relationship, our owner instance needs an empty array to store its collection of items (in this case, dogs), where every instance of the dog that's instantiated can be added. 

```ruby
class Shelter
  attr_accessor :dogs, :name

  def initialize(name)
     @name = name
     @dogs = []
  end
end
``` 

Here, we're just setting up a new shelter named brooklynshelter:

```ruby
brooklynshelter = Shelter.new(brooklynshelter)
=> #<Shelter:0x000055a164d8b1d8 @name=nil, @dogs=[]>
``` 

We're going to reset our dog (belongs to) and shelter (has many) relationship.

```ruby

brooklynshelter = Shelter.new(brooklynshelter)
snacks = Dog.new
snacks.shelter = brooklynshelter
snacks
=> #<Dog:0x00005614828bf708 @shelter=#<Shelter:0x00005614828bf758 @name=nil, @dogs=[]>>

```
So, we can that snacks now belongs to brooklynshelter, an instance of Shelter, which has a collection (empty array) of dogs. 

```ruby
brooklynshelter.dogs
=> []

``` 

When we ask brooklynshelters for its dogs attribute, it's still showing up as being empty. Because there's another essential step we're forgetting: ADDING THE INSTANTIATED DOG INTO THE EMPTY ARRAY. We're going to do that with an #add_dog method

```ruby
brooklynshelter = Shelter.new(brooklynshelter)
snacks = Dog.new
snacks.shelter = brooklynshelter

brooklynshelter.add_to_shelter(snacks)
brooklynshelter
=> #<Shelter:0x0000563fc0797240 @name=nil, @dogs=[#<Dog:0x0000563fc07971f0 @shelter=#<Shelter:0x0000563fc0797240 ...>>]>
```

Now, the flip side of the relationship—the has many relationship—is complete. The instance of Shelter—brooklynshelter—knows it has a dog instance whose shelter attribute is equal to the shelter. During my dazed-and-confused days, I found that seeing the return values of instances really helped cement my understanding of relationships. 

**Has Many Through Relationship
**

One way I get my brain to comprehend complicated Ruby concepts is by breaking them down into simple rules or its smallest components. I’m going to try that, here, with the has many relationship. 

The **has many relationship** describes the connection between 3 classes, wherein 1 of 3 classes provides an indirect link (or relationship) between the other 2. 

- One item will be the middle man and provides an indirect relationship between or through two objects 
- The shared item will belong to the other two items
- The other two items will have many of the shared item

For example:

                 ----> dog ----> owner
shelter   ----> dog ----> owner
                 ----> dog ----> owner
								 
								 
In this relationship:
* shelter has many dogs
* dog belongs to shelter and owner
* owners has many dogs 
* *through* dogs, shelter has many owners and owners has many shelters


```ruby
class Shelter #has many dogs
  attr_accessor :name, :city
  @@all = []

  def initialize (name, city)
    @name = name
    @city = city
    @dogs = []        
    @@all << self
  end

  def add_dog(dog) #always should have an argument so we can pass in an instance of dog
    dog.shelter = self
    @dogs << dog
  end

  def dogs
    @dogs
  end

  def self.all
    @all
  end
end

class Dog #belong to a shelter & an owner
  attr_accessor :name, :age, :breed, :shelter, :owner
  @@all = []

  def initialize (name, age, breed)
    @name = name
    @age = age
    @breed = breed
    @@all << self
  end

  def self.all
    @all
  end
end

class Owner #has many dogs 
  attr_accessor :name, :age, :dogs
  @@all = []

  def initialize (name, age)
    @name = name
    @age = age
    @dogs = []
    @shelters = []
    @@all << self
  end 

  def add_dog(dog)
    @dogs << dog
    dog.owner = self
  end

  def shelters
    self.dogs.each do |dog| 
    @shelters << dog.shelter if dog.shelter
    end
    @shelters
  end
    
  def self.all
    @@all
  end
end
```

With all this, we can invoke:

```ruby
ruffles = Dog.new("ruffles", 1, "corgi")
queensshelter = Shelter.new("Queens Humane Society", "NYC")
ruffles.shelter = queensshelter
ruffles.shelter
queensshelter.add_dog(ruffles)

joe = Owner.new("joe", 30)
joe.add_dog(ruffles)


joe.shelters
joe.shelters.each {|shelter| puts shelter.name}
=> Queens Humane Society
=> [#<Shelter:0x00005612a3437d38 @name="Queens Humane Society", @city="NYC", @dogs=[#<Dog:0x00005612a3437db0 @name="ruffles", @age=1, @breed="corgi", @shelter=#<Shelter:0x00005612a3437d38 ...>, @owner=#<Owner:0x00005612a3437cc0 @name="joe", @age=30, @dogs=[#<Dog:0x00005612a3437db0 ...>], @shelters=[...]>>]>, #<Shelter:0x00005612a3437d38 @name="Queens Humane Society", @city="NYC", @dogs=[#<Dog:0x00005612a3437db0 @name="ruffles", @age=1, @breed="corgi", @shelter=#<Shelter:0x00005612a3437d38 ...>, @owner=#<Owner:0x00005612a3437cc0 @name="joe", @age=30, @dogs=[#<Dog:0x00005612a3437db0 ...>], @shelters=[...]>>]>]

```




