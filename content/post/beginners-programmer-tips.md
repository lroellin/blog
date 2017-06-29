+++
title = "Beginner Programmer's Tips"
date = 2015-02-25T14:33:35+02:00
+++

This is for everyone out there who wants to start programming. This isn't about my story, how I learned it, that will be another post. This is about common mistakes you made (and it's actually good you make it) and how to avoid them later on.
# About mistakes
We're learning everywhere that human beings make mistakes and that this is bad. I'll tell you something: as long as you're not a doctor, or do any other work where people's lifes depend on, it isn't. In fact, it's great you make mistakes in the beginning. I've never learned more than when I followed a tutorial and something went wrong. You know, the ones where the teacher does something and you program along and then suddenly, what the computer tells you is different from what it's supposed to be, or it doesn't work at all. When you're starting, these are mostly syntax errors, like mixing up "=" and "==". By then, you'll have two options

* Ask someone else. If you're in a classroom, ask a mate or if you're not, google the error. This is how you could do it, but if you run into the same problem twice, do it the second way which is
* Try to fix it yourself

The second one is better for you, since instead of just typing you learn what is really done in each step and you'll learn some troubleshooting techniques along the way. Classroom bonus task: Ask your teacher to do mistake presentations, which is a weird thing in the first place, but you'll learn to appreciate it later. At the end of each lesson, or each day, whatever, each has to showcase what he or she did wrong and how they got to the solution. It's not embarrassing, since other students will do the same mistakes and it's helpful for the others, because they can see how to fix such mistakes. Ok, let's start with the more technical tips.
# Double characters
When programming, you'll often encounter part of the syntax, that needs to be in pairs. Like parentheses "()", double quotes, single quotes, stuff like that. You may have seen some monster like this and asked you. How did they do that?

```cpp
if ((a+b == 3 && (c+d <= 5) || a+b == 5) && x+y == 8)
# don't try to understand this, it's completely made up
```

The key to those monsters is doubling characters ahead. Whenever I write an opening parenthese, I also write a closing one. So at the start, if actually looks like this

```cpp
if ()
```

and then it evolves

```cpp
if (a+b == 3 && ())
```

and so on. Do the same with every character that is a divider of some sort and you'll make less mistakes. I even do this when writing normal texts (such as this) although it looks weird to anybody not involved.
# = and ==
This is a source of problems for a lot of beginners. This causes all sorts of problems. When you assign a variable with (`$a` is a variable called "a" in most languages)

```cpp
$a == 3
```

then your compiler will complain. But if you do a test with

```cpp
if ($a = 3)
```

it will always return "true" because the assignment was successfully made and is therefore fine. Personally, I too had a bit of a problem with that. You have to know the difference by heart. Rule of thumb: if there are any double-parentheses around, double the equation sign too.