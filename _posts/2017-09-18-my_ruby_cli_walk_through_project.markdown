---
layout: post
title:  "My Ruby CLI Walk Through Project"
date:   2017-09-18 16:48:27 -0400
---

**What is Cryptocurrency?**

A cryptocurrency is a digital or virtual currency that uses cryptography for security. A cryptocurrency is difficult to counterfeit because of this security feature. A defining feature of a cryptocurrency, and arguably its most endearing allure, is its organic nature; it is not issued by any central authority, rendering it theoretically immune to government interference or manipulation.

The first cryptocurrency to capture the public imagination was Bitcoin, which was launched in 2009 by an individual or group known under the pseudonym Satoshi Nakamoto. As of September 2015, there were over 14.6 million bitcoins in circulation with a total market value of $3.4 billion. Bitcoin's success has spawned a number of competing cryptocurrencies, such as Litecoin, Namecoin and PPCoin.
<a href="http://www.investopedia.com/terms/c/cryptocurrency.asp">Source</a>

**Deciding on a topic**

I hold a few cryptocurrencies and I wanted an easier way to be able to see the current market price of those cryptocurrencies. There are a lot of websites that provide current market price for the currencies  and one such website is coinmarketcap.com, which has all of the cryptocurrencies indexed, ordered from highest to lowest market cap, with various information in dollars. However, I’d still need to open up a web browser, scroll down to see the current price of the currency. I needed a way to get the current price faster which is why I decided to build my CLI project on cryptocurrencies.

**Getting Started**

The guidelines were simple:
1. Package as a gem.
2. Provide a CLI on gem installation.
3. CLI must provide data from an external source, whether scraped or via a public API.
4. Data provided must go at least a level deep, generally by showing the user a list of available data and then being able to drill into a specific item.

This was my first project and I was not quite sure how to begin. After watching Avi’s Daily Deal video walkthrough it helped me get me started. Avi's video helped me create the basic framework and I was able to see the methodology behind creating a program from scratch. I used gem bundler to create a gem, Nokogiri ruby gem and Ruby’s built-in ‘open-uri’ to scrape the information from the website.

I modeled my project to take a user input and display the currency name, price and market cap for all of the top 10 currencies or just one. One of the files is currency_price.rb file where I scrape the website to pull the required data and another is cli.rb where I create my user interface where users can enter one of the available selection to see individual currency price or all of the top 10 currency price by marketcap. I used an if/else statement to take the input and direct it at the method that will show the information based on their selection. After the information is displayed it would give the user the option to make another selection or to exit the program.

**Challenges**

Most of the challenges that I faced in this project revolved around getting the data to show up the way that I wanted. First challenge was getting first 10 currencies from the website. After much research, I was able to get the list of the first 10 currencies including the names, prices and market cap values by adding first(10).

```
doc = Nokogiri::HTML(open("https://coinmarketcap.com"))
     currency = self.new #initialize new currency
     currency.name = doc.css("td.currency-name a").map{|a| a.text}.first(10)
     currency.price = doc.css("td.no-wrap a.price").map{|a| a.text}.first(10)
     currency.marketcap = doc.css("td.market-cap").map{|marketcap| marketcap.text.strip}.first(10)
     currency
```

Second challenge was to get the currency name, price and market cap of only one currency when the user enters in a number between 1 – 10. The third challenge was to account for invalid input if user enters anything besides numbers 1 - 12 or exit the program. After a lot of testing, I finally decided to use Each method inside an If statement and another nested If statement inside the Each method.

```
input = gets.strip.to_i
    if input.between?(1,12)
      crypto.each do |currency|
        if input == 11
          puts currency_list
          menu
        elsif input == 12
          puts "Good Bye!"
        else
          puts "#{currency.name[input - 1]}: #{currency.price[input - 1]} - #{currency.marketcap[input - 1]}"
          menu
        end
      end
    else
      puts "Invalid input please enter number between 1 - 12"
      menu

```
    

I am glad I was able to overcome the challenges I faced and accomplish everything I wanted to do. I would like to have the user enter ‘list’ to see the list of top 10 currencies or exit to exit the program, but since the return from gets is always a string I found this to be the solution for the time being and ask the user to enter number 11 to get a list of currency and 12 to exit the program. I may make this enhancement in the future.


