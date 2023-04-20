---
title: "Regular Expressions"
author: 'shortjij'
categories: ["4PL3 Final Project"]
---

One thing I made using regular expressions is a function which will count the words and vowels that input has. This would be very helpful and buildable for a linguist to use if they need to investigate a corpus. 
```{r}
string_info <- function(input){
  if(is.character(input) == TRUE){ 
    tolower(input)
    paste(tolower(input), "is a character with", stringr::str_count(input, "\\b\\w*\\b\\s"), "word(s) and this input has", stringr::str_count(input, "[aeiou]"), "vowels")
  } else if(is.character(input) == FALSE){
    print("invalid input")
  }
}
about('today is a beautiful day')

```


