---
layout: post
title:      "Understanding object-oriented ruby relationships"
date:       2018-09-25 16:13:05 +0000
permalink:  understanding_object-oriented_ruby_relationships
---

As a beginner programmer, I had the hardest time wrapping my head around the concept (and formatting) of object-oriented relationships in code. It literally took weeks of reading explainers on blogs and watching OO Relationship tutorial videos. Here, I’m going to distill examples of belongs to, has many, and has many through relationships down to the nitty gritty, which helped me comprehend the concepts. Hopefully, it’s useful to you too. 

**# Belongs to relationship**

The belongs to relationship means that ONE object (songs, dogs, etc.) has an owner (artist, shelter, pet owner, etc.).


```ruby
  class Song
	  attr_accessor :artist
		end
```
