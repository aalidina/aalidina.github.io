---
layout: post
title:      "Sinatra Project- Crypto Market"
date:       2018-04-14 18:39:54 +0000
permalink:  sinatra_project-_crypto_market
---



The projects requirements are:

* Build an MVC Sinatra Application.

* Use ActiveRecord with Sinatra.

* Use Multiple Models.

* Use at least one has_many relationship.

* Must have user accounts. The user that created a given piece of content should be the only person who can modify that content.

* You should validate user input to ensure that bad data isn’t created.

* Any validation failures must be shown to the user with an error message.


A few years back I started trading in Crypto Currency, so I decided that for my Sinatra final project I would create a simple app which would allow users to see current prices of all crypto currencies and allow them users to add the currencies to a list. 

The hardest part was to figure out how to build a web form that would allow a user to select the currencies that they want, add then to the list and to display the user's selected currencies on the next page. I had to go back and revisit previous lesson Sinatra RESTful Routes which help me built a form that would give me that parameters that I could use to save the users choices to the database and display them on the next page.

After creating a form that would allow a user to choose currencies and add them to a list the second issue that I ran into was that the page which was supposed to show the currencies user had selected would only show the first currency. This was due to how the route was setup in the controller and to over come this issue I had to create a list page instead of a show page which would render all the currencies user selected.

If you want to take a look at the code you can find it on [GitHub](https://github.com/aalidina/sinatra_crypto_app). I would really appreciate any feedback you can offer.

Happy coding!




