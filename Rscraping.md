---
title       : "Scraping with R"
subtitle    : Test subtitle
author      : "Eugene Pyatigorsky"
job         : Ahalogy
framework   : revealjs
revealjs    : {theme: night}
highlighter : highlight.js
hitheme     : Github 
widgets     : []
mode        : selfcontained
knit        : slidify::knit2slides
---





# Scraping with **R**

<br><br><br><br>
<footer>
Cincinnati R Users Group<br>
June 21, 2016  <br><br>
**Eugene Pyatigorsky**
<br><br>
This presentation and supporting materials available at:<br>
https://github.com/epspi/Rscraping
</footer>

---

## Agenda
* Overview of packages
* A look at how to scrape
* Working example
* Best practices

--- .chapter

# Overview of packages 

--- &vertical
## rvest

Most of the work will be done by Hadley's package `rvest`

* Based on Python's `beautifulsoup`
* Extracts elements from the dom using CSS or XPath

.fragment **e.g.<br>`rvest::read_table()`**

***

##  httr

This is (Hadley's) wrapper for `curl`

* Really useful for making customized calls to APIs
* Can also be used for writing your own APIs

.fragment **e.g.<br>`httr::GET("some_endpoint", config)`**

--- .chapter

# How to Scrape: An Example

--- &vertical
## Let's ask Bing about the R Users Group


```r
lnk <- 'http://www.bing.com/search?q=Cincinnati+R+users+group&go=Submit&qs=n&form=QBLH&pq=cincinnati+r+users+g&sc=0-20&sp=-1&sk=&cvid=4A13A7CB066B419B9F7BD75777D68F09'

read_html(lnk) %>% 
    html_nodes("h2 a") %>% 
    html_text
```

```
## [1] "Cincinnati UC Users Group (Cincinnati, OH) - Meetup"        
## [2] "Local R User Group Directory - Revolutions"                 
## [3] "New R User Group in Cincinnati / Dayton - Revolutions"      
## [4] "Cincinnati Sharepoint User Group - Facebook"                
## [5] "Cincinnati .Net Users Group"                                
## [6] "CincyPowerShell | PowerShell Community Groups"              
## [7] "Reinaldo R. - Cincinnati UC Users Group (Cincinnati, OH ..."
## [8] "Group: Cincinnati |Tableau Support Community"
```

*** 

## Common CSS Selectors

* `#` for "id="
* `.` for "class="

.fragment **OR you can use SelectorGadget for Chrome**
<br>
https://chrome.google.com/webstore/detail/selectorgadget/

--- .chapter


# A Working Site

--- &vertical

[Cincinnati Foreclosures - A Real Estate Scraper](http://cincyreal.followthenumbers.com)

--- .chapter


# Best Practices

--- &vertical

## Authentication

Use APIs instead of scraping whenever possible. There isn't a lot of documentation for `rvest` and cookie-based authentication can be tricky.

***

## Automation

* The real power of `R` and `rvest` shines when used with `shiny` (npi).
* Put your scraping code in a standalone R script and automate with `cron`. 

***

## End
