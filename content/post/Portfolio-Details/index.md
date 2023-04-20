---
title: 'Swirl Course on ForLoops'
author: Juliana
date: 2023-01-21
categories: ["4PL3 Final Project"]

---

I have also created a **swirl lesson on forloops**, this was created to be a quick, interactive way for people to learn how to use forloops. I have made one lesson so far, which talks about the syntax of a forloop and making sure that is 100% clear. The next installment will be more interactive and focus on creating forloops from scratch. 

```
- Class: cmd_question
  Output:  copy this code; for(i in 1:10){ print(paste("this number is", i))}
  CorrectAnswer: for(i in 1:10){print(paste("this number is", i))}

- Class: mult_question
  Output: How would we format the first part in a forloop if we wanted to only look at the numbers from 1 to 20
  AnswerChoices: for(i in 1:10);for(1 in 20); for(i in 1:20)
  CorrectAnswer: for(i in 1:20)
  AnswerTests: omnitest(correctVal= 'for(i in 1:20)')
  Hint: remember that using x:y character means you created a sequence from x to y. Also remember i is a placeholder. 

- Class: mult_question
  Output: If we wanted to add 1 to a vector of numbers, how could we format that inside the for loop?
  AnswerChoices: i + 1;vector + 1;sum(vector)
  CorrectAnswer: i + 1
  AnswerTests: omnitest(correctVal= 'i + 1')
  Hint: Remember i is a placeholder for ONE INSTANCE in the vector.

- Class: text_question
  Output: write a forloop if you wanted add 1 to each number in the sequence 1:10. The format should be for(i in ____){print(__ + 1)}
  CorrectAnswer: for(i in 1:10){print(i + 1)}
  AnswerTests: omnitest(correctVal='for(i in 1:10){print(i + 1)}')
  Hint: maybe try this, for(i in 1:10){print(i + 1)}

```
