---
layout: post
title:      "Achievement Unlocked: First Big Coding Project"
date:       2018-08-10 20:10:09 -0400
permalink:  achievement_unlocked_first_big_coding_project
---


I’ve finished my first portfolio project, [the CLI data gem](https://github.com/DMCatanach/burque-trails-cli-app), and I’m pretty proud of it. The website I chose to scrape with wasn’t the most straightforward to work with, presenting some interesting challenges, but I (mostly) figured it out. I started with an idea about a task I wanted to be able to accomplish, and now I have a program that does that very thing.


My idea started with one of my hobbies - running. I took it up a couple of years ago, starting off with running and walking intervals (though, truth be told, that’s still where I am). Initially, I used routes around my neighborhood and a nearby bike path (which connects with [a route](https://m.strava.com/local/us/albuquerque/running/routes/1365?hl=en-US) that apparently [runners travel here to train on](https://medium.com/great-runs/great-runs-in-albuquerque-new-mexico-b9bc56e80a6c)). More recently, I’ve discovered that some of the parks in my city have [paved trails, or simply established routes for walking and running](http://www.cabq.gov/parksandrecreation/parks/prescription-trails/list-of-trails), so I’ve taken to exploring these to shake up my routine a bit.

	
If you visit that link to the list of the trails, you may notice there isn’t actually a list, but a map with pins that open a popup that link to a page about the park at that location. In addition, the “Find a trail by zip code” section has a link to one zip code, and does not allow any searching. So, I wrote my data gem to do exactly that: search for one of these trails by zip code. At first, I wasn’t sure if that was going to be possible, because of the map’s setup. But, I discovered that there is a base url such that, with a zip code appended to it, will open a page for that zip code with a list of the parks in it. That simplified matters a lot!

	
When my program runs, it asks the user for a zip code, uses that input to open the appropriate page (for example, [this one](http://www.cabq.gov/parksandrecreation/parks/prescription-trails/87109)) then scrapes it for the names of the parks and their urls and displays a numbered list of the names. This information is also stored as a park object with name and url attributes.  The user can then chose to see details about one of the parks on that list. If so, the program asks the user to put in the number on the list of the park they want to know about, converts that number to an index corresponding to that park object from an array of all park objects. Then it opens that park’s url and scrapes details such as a description of the park and its cross streets. I wanted to also include information about the trail, such as the distance, but scraping that information is a tricky problem that I haven’t yet solved.


There were some other tricky issues involved. I had to write three different methods to scrape the details and include some conditional logic to call these from the command line interface because although each individual park’s page lists the same information (most of the time - some don’t have descriptions), they don’t all have an identical HTML structure. Two of them have unique structures. I knew about one of them before I started writing the detail scrapers, but the other one was, unfortunately, the one I first used when trying to write the scraper that would handle most cases.


It seems like I spent nearly as much time combing through the website to figure out how to execute my idea as I did coding the program. Once I found that there exist pages listing parks by zip code, even if there’s no easy way to access them by navigating the site, I went through each zip code in Albuquerque, checking to make sure of which ones would open a page instead of running into a 404 error so that I could build in validation for the zip code input by the user. Then, when I discovered that my detail scraper broke when I tried to use it on a different page than the one I’d written it for and it was clear that I had another exceptional case, I surveyed other pages to see if there were any other exceptions. There weren’t, but finding out was certainly painstaking and somewhat time-consuming. It was worth it, though, to build something that doesn’t break all the time. 


Now I have a program that does most of what I wanted it to do - look up park trails by zip code - and I even use it to choose new spots to explore. I’ve also added the option to see a list of all the trails. After a couple of rounds of refactoring, I still have some ideas for some functionality to add later, like opening the page for a park and choosing one at random. Mainly, though, I want to make a web app out of it, using [open data](http://www.cabq.gov/abq-data/), and including bike and hiking trails as well. 

