---
title: "Search text by patterns in R"
layout: post
date: 2018-12-10 16:00
image: /assets/images/textR.png
headerImage: true
tag:
- text
- data mining
- R
star: false
category: blog
author: oldiya
description: Blogpost
---



I have been lucky enough to get all my masive data in nice formats, but this past months I had to extract information from tables that were exported as text. This is not a very complicated thing to do but it was new to me to have a code that will do this, so here we go: 

I have re-created the information in a text file that you can find [here](https://olalladiaz.net/assets/data/tableresults.txt). The first thing I am going to do is to load the strings from the text file, I used the encoding "latin1" because the text contained latin characters that otherwise would not be correctly read. 

```R
   
#filepath = "Data/tableresults.txt"
strings <- readLines (filepath, encoding = "latin1")
    
```

I was interested in only selecting certain parts of the text, there was two way I could do this: 1) I could just select the line I was looking for: 

```R
   
strings [6]
    
```

In my example the information was a text table with rownames, in this case it was easier to find the row name and select it by the name by identifying the text pattern in the strings.  

The function *grep()* identify the pattern within each element of a character vector. Since the whole row was considered as one character vector I also used *strsplit()* to divide each of the columns by splitting the elements of the character vector into substrings.

In this example I am looking for the values for the "Roundwood volume" row:

```R
# Check all the strings and looks for the row with the pattern "Roundwood volume"
roundwoodVol <- unlist (strsplit (strings[grep ("Roundwood volume", strings)], "\\s+"))
roundwoodVol <- as.numeric(roundwoodVol [5:length (roundwoodVol)])   
```

Here you go! If you have a more clever way of doing this, I'll be happy to hear! 
