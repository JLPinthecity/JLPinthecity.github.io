---
layout: post
title:      "How to Start and Finish Your CLI Portfolio Project"
date:       2018-11-30 17:16:26 -0500
permalink:  how_to_start_and_finish_your_cli_portfolio_project
---


The hardest part of finishing my CLI project was starting it. (Just like every creative venture, I guess!) After completing the labs in the final-projects portion of Object Oriented Ruby, I had no clue how to start. Overall, it took me nearly four weeks of review and prep to complete my CLI project. Completing the OO Ruby section labs, I knew the next step for me was reviewing my study notes for procedural and OO Ruby (four notebooks worth). Before starting my CLI project, I wanted to refamiliarize myself with all the tools (err, methods) in my coding toolkit. 

***Brainstorming an idea and finding the perfect website to scrape***

When I presented my CLI-app idea to my assigned Flatiron School technical coach, I thought I’d end up scraping Goodreads. For my project, I wanted to work with a books list. Because scraping a book list and then scraping an individual book landing seemed like a simple way to fulfill the project requirement for going one level deep and grabbing further details. In this case, the user would be prompted to choose a book from the list to learn more about. 

After scraping Goodreads (and having a pretty hard time to scraping details within the individual book link), I learned finding a great website to scrape is truly half the battle. So I started looking at other options. I knew I was onto something when I landed on Penguin Random House’s page for Award Winners in Fiction page. The page was formatted neatly in a way that other websites I’ve seen successfully scraped in Instructable and YouTube tutorial videos. 

Inspecting elements for several books, I noticed the backend was pretty organized and contained uniform tags (hallelujah). So it was pretty much decided. For my CLI project, I’d be scraping[ Penguin Random House’s list of award-winning fiction](https://www.penguinrandomhouse.com/books/award-winners-fiction). Wahoo. 

***Start coding***

I had so many questions. Mostly “where?” and “how?” pertaining to my project. Since starting Flatiron School’s online full-stack program, I’ve only used Learn IDE to complete labs. I had no clue whether I should code in Learn IDE or set up a local environment for the project. After setting up a git repository on GitHub [using this video](https://www.youtube.com/watch?time_continue=317&v=YZNXWWHUO-E), I was able to create an in-browser set up. 

Before starting my project, I read up on basic CLI setup and format—what goes in an environment file, what happens in bin/console, and how to require all your lib files. I probably didn’t need to stress because using Bundler to generate and manage a gem automatically provides you with a general set up. 

After that, I found Avi’s [CLI Walkthrough video](https://www.youtube.com/watch?v=_lDExWIhYKI) super duper helpful. I was able to literally follow his step-by-step instructions for setting up a gem, creating an executable file, setting up an environment file, and requiring pry and Nokogiri in your gemspec, to get started. Plus, I found his explanation of the process really helpful as a starting point. The gist: At the beginning, it’s helpful just to start coding. If you don’t know where to start, consider the starting point for the user, which would probably be the executable file. 

***Determine your classes and what your objects will consist of***

From the get-go, I knew I’d have three classes guided by the single responsibility principle:

CLI class: That’s in charge of user input—and calling on methods in the other two classes that present the full books list, accepts user input, and displays further details about each book. 

Scraper class: Deals with all the necessary scraping tasks, culling website data from Penguin Random House to make up the main books list and for the individual book details

Book class: To instantiate all my book instances and hold my collection of book objects in the @@all variable. 

In my project, each book object represents a book on the Award-Winning Fiction Books list. Every book has the same set of attributes: title, author, and url (for me to grab and scrape for further details). Further details include the specific category of fiction, book description and additional author details. 

***Plan the flow of your CLI app***

In order words, envision what you want the user to experience. Here’s what I planned my gem in my Notes memo.

CLI portion:
“Welcome to the Top Books of 2018 Bookfinder App.”
Display list. 
“Enter the number of the book you’d like to learn more about. Enter exit to leave the program.”
Options: 
If out-of-range number is entered, display the list again. 
If input == existing number, display Learn More Menu for Book 
Learn More Menu for Book 
Author
Genre
Description
Goodreads link 
If exit, exit program. “Thank you for using the Top Books of 2018 Bookfinder App. Goodbye!”

Learn more menu for book: 
Author
Genre
Description
Goodreads link 

“Want to learn more about the book?”
If yes, display Learn More Book Menu
If no, display full book list with option to exit. 
In the end, my CLI app is reflects this action plan but is actually much more simple. After talking to my technical coach toward the end of project, I decided that I would be beneficial to not pursue the extra features and to simply get the project that checks the basic list of requirements submitted.

***Anticipate feeling stuck in code + my solution for getting unstuck ***

While coding, I experienced two pain points—trying to figure out how to get the books to display in a numbered list and getting the additional book details to appear after scraping the individual book URLs. 

When I couldn’t figure something out, I’d watch CLI gem walkthroughs on [Learn Instruct](https://instruction.learn.co) and keep an eye on the patterns that would arise, particularly, how classes were relating to each other. This provided me with many clues that helped me solve the issues in my CLI app. 

I was able to display the numbered list of books using the #each.with_index method and then finally got my individual-book details to show up after taking out the until/while loop and using an if/else statement. Then I realized my book details weren’t showing up because I had forgotten to assign the values to the individual book after scraping the each value in my scraper method. 

Take a look at my code [here](https://github.com/JLPinthecity/bookfinder). 


