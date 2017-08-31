+++
title = "Python for Java Programmers - Getter and Setter"
date = 2017-05-05T16:32:10+02:00
+++

I'm currently in the process of learning Python. What I know is Java and C# and some script languages like PowerShell. I want to tell about my journey a bit since you're getting in a kind of culture shock when going from Java to Python

In Java, the compiler does a great job at keeping you from doing stupid things. In Python, that's up to you since the script is loaded as needed (not exactly in the technical meaning) and run from top to bottom (again, not exactly technically). And because all that happens quite fast and you don't spend much time on it, the compiler won't check such stuff for you before this code is executed.

I found a nice quote about this from The Benevolent Dictator: "We're all consenting adults". So it's your job to keep an eye on what you access and if that's possible. However keep in mind that IDEs do a great job of telling you these things, but it's not the default for a Python installation.

Now for the first thing we're gonna look at: getter and setter. This will be me paraphrasing [this video](https://archive.org/details/SeanKellyRecoveryfromAddiction).

In Java, again, you write a class and put in private attributes. You then write a constructor and public getter and setter for that (ok, your IDE does). This is to stop you from breaking the encapsulation. And if you want to validate something on the setter, then you have a single place to change.

However, how many times did you actually change the setter? For me, coming from C# (which sorta has what I'm gonna show you for Python, Properties), getter and setter are noise in a class. I skip them while reading your class and that means I will skip your validation scheme on one important attribute.

Now the alternative would be to set it all public and when the time comes, change it to a private attribute and a public getter and setter. But now you have to change all client code (code that calls your class) and that can turn into a nightmare, especially if you're developing a library and now every single piece of code using the updated version has to change. There sure are better methods, tools or frameworks for this, but I currently don't know any.

In Python, the story is a bit different. You don't actually declare your attributes, since (what I've grasped so far), definition is declaration in Python. So what you'll do is initialize your parameters in the constructor just so you have a name you can all agree on. Then you'll just access those attributes from the outside.

Now what if you have to validate your attribute on a later version: well, Python has you covered there. You simply define your attribute as a property, define getter and setter for that, and store the actual attribute as _attribute. The underscore is the <i>convention</i> that others should not touch your attribute. Remember, we're all consenting adults. Then, no client code needs to be touched (except of course when it now breaks your validation but it's no syntax error or the like.

How do you do that? Let me close this post with just a bit of code [coming straight from StackOverflow](http://stackoverflow.com/a/2627034).

Before

```python
class BigX(object):
    def __init__(self):
        self.x = None

# Getting and setting
o = BigX
o.x
o.x = 5
```
After:
```python
class BigX(object):
    def __init__(self):
        self._x = None
    @property
    def x(self):
        print "getter of x called"
        return self._x
    @x.setter
    def x(self, value):
        print "setter of x called"
        self._x = value

# Getting and setting
o = BigX
o.x # "getter of x called"
o.x = 5 # "setter of x called"
```