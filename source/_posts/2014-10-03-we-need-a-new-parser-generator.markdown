---
layout: post
title: "We Need a New Parser Generator"
date: 2014-10-03 10:30:49 -0700
comments: true
categories: 
  - Parser Generators
---

I think it's about time for a new parser generator.

Yes, I realize that words to this effect have caused more tears than Old
Yeller, and have been the source of more than a little of the world's
[digital ills](http://xkcd.com/927/), but I'm pretty sure I'm speaking the
truth.

The problem, in short, is that the collection of today's most popular parser
generators each suffer from one of two problems:

*   *Fragile parsing specifications*:
    Most parsers that are based off of the LR or LL parse algorithms have an
    inherent limitation or two. In the former, its the inability to deal with
    possibly benign shift-reduce (or less benign reduce-reduce) conflicts. In
    the latter, it's the relatively spotty support for left recursion. In each
    case, the grammar writer is forced to contort their specification into a
    form which the parser generator can deal with, making the specifications
    themselves potentially much harder to read.

*   *Specifications are tied closely to the implementation language*:
    Practically every parser generator I've seen (except for possibly the
    [GOLD parsing system](http://goldparser.org/)) ties itself inextricably to
    some implementation language. YACC, ANTLR, JavaCC all assume that you will
    write your semantic actions inline in the language of your choice. Of
    course this means that if someone wants to parse your language in another
    implementation language, they'll have to likely recreate it from scratch,
    or rewrite a good deal of it.

In addition, there is one thing which I have never seen in a parser generator
outside of a few research tools: *modularity*. For those language developers
out there: how many times have you had to write the normal chain of binary
mathematical operator expressions? How many times have you had to write
a repeating list of elements? You may have even had to pull one parser into
another in order to support embedded languages. Why shouldn't we be able to
package up all of these boring and cluttering pieces of boilerplate into some
library, and just reuse the crap out of it? That is considered good computer
science, right?

I would very much like to write just such a tool, which fixes all of these
issues. Previously, the biggest issue was the problem of fragile parsing
specifications above, but extensions of the Earley parse algorithm such as
[Marpa](http://jeffreykegler.github.io/Marpa-web-site/) seem to have solved
the core efficiency problem, while providing the necessary flexibility.

At the moment, I'm calling my yet-to-be-created parser generator Boar. Future
articles will go into more detail about different aspects of the tool, and how
it will work.
