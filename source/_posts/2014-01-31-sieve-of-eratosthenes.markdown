---
layout: post
title: "Sieve of Eratosthenes"
date: 2014-01-31 21:03:29 -0500
comments: true
categories: 
---

So I've been taking an interest in prime numbers recently and how to generate them, so I wrote a up a quick implementation of [The Sieve of Eratosthenes](http://en.wikipedia.org/wiki/Sieve_of_Eratosthenes) in Python. Here it is:

``` python
def primes(n):
  candidates = []
  for i in range(2, n+1):
    candidates.append([i, False])
  p = 2
  sieve(candidates, p)
 
def sieve(candidates, p):
  done = False
  while(not done):
    for pair in candidates[p-2::p][1:]:
      pair[1] = True
  
    found = False
    rest = candidates[(p-2):][1:]
    for pair in rest:
      if not pair[1]:
        p = pair[0]
        found = True
        break
   
    if not found:
      done = True
    
  for pair in candidates:
    if not pair[1]:
      print pair[0]
```

For those interested in more curious facts about prime numbers a brilliant talk is given by the great Terrence Tao. It's a bit lengthy but [well worth your time.](http://www.youtube.com/watch?v=PtsrAw1LR3E)
