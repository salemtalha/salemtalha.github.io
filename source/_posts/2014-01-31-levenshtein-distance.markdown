---
layout: post
title: "Levenshtein Distance"
date: 2014-01-31 22:21:01 -0500
comments: true
categories: 
---

I was reading on wikipedia about a few string functions and one interesting 
one that I came across is the [Levenshtein Distance](http://en.wikipedia.org/wiki/Levenshtein_distance).
It's a really neat way of figuring out the "edit distance" between two strings,
and, like many problems, it's best stated recursively. So here's my
implementation in racket. It's always interesting to think about how some
problems almost beg to be solved via a particular paradigm, and I think this is one of them.
For comparison, the imperative solutions on the wiki page are quite long and a
bit unwieldy.  

``` racket
(define (reallev str1 str2)
  (define cost 0)
  (cond [(empty? str1) (length str2)]
        [(empty? str2) (length str1)]
        [else
           (when (not (equal? (first str1) (first str2))) (set! cost 1))
           (min (add1 (reallev (rest str1) str2))
                (add1 (reallev str1 (rest str2)))
                (+ (reallev (rest str1) (rest str2)) cost))]))

(define (lev str1 str2) (reallev (string->list str1) (string->list str2)))
```

Some cool uses of this might be, for example, to suggest spelling corrections on devices. If
you misspell a word, chances are the one you want is a short number of edits away, which in this
algorithm is formalized as being either a insertion, deletion or replacement.

The gist of the algorithm is quite simple. You start off comparing the strings pairwise.
As seen in the recursive call at the end of a function, if the two characters being 
compared do not match, you're trying to achieve the minimum of of the 3 strategies by attaching a 
"cost" to each operation and allowing each scenario to be recursed upon. It's quite elegant, and to me
it turned out to be simpler than I assumed it to be.
