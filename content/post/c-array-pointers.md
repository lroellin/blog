+++
title = "C arrays are just better pointers"
date = 2017-07-03T19:28:07+02:00
draft = true
+++

This post will be about how arrays work in C, at least to the point that I know of yet. It helped me understand things better on how they even work and I just wanna share this in case someone has the same problems I had :) As always, because C is so complex, I'll tell you enough to be dangerous, but not much more. There probably is another layer of abstraction behind all this...

Ok, so you all know arrays. They're taught to us as a series of variables of the same type. You gotta know beforehand how many you want[^1]. Here's an example of initializing array of 5 `int`s.

```cpp
int numbers[5];
```

Now you may have heard before, that C does not know how big your array really is. That is why it's so easy to just keep writing past your array. If that something behind your array belongs outside of your program, you're in luck - the OS is gonna shut your program down for accessing stuff outside its memory. If not, you overwrite something of your own stuff and you won't even notice.

Well, why is that? I just told C that my array has a size of 5?!

You have to know here, that an array is just a better way of expressing and accessing pointers. We call that syntactic sugar. 

Basically, `numbers` is a pointer of type `int`, pointing to the *first* element in that array. So

```cpp
numbers[0];
*numbers;
```

are the same. `numbers` is just the memory *address* of the first element.

Now how does this help? Well, these two are also the same:

```cpp
numbers[x];
*(numbers + x);
```

(The parentheses are just there for clarifying syntax, otherwise the result would be whatever's at `numbers` plus the number `1`.)

So how does this work with memory? The way I always understood it, is: let's say `numbers` is at memory address `0x800`. And let's say, `int` is 4 bytes long (32 bit, remember this is C so it's not set), which you can get by `sizeof(int)`.

That way, `numbers[x] will always lie at `0x800` + `x` * 4. So `numbers[1]` is at `0x804`, `numbers[2] is at `0x808`, and `numbers[4]` is at `0x810` (remember, this is hexadecimal).

Or, more general (`array` and `n` are arbitrary)

```cpp
TYPE array[n];
array[x];
```

lies at memory address of `array` + `sizeof(TYPE)` * `x`. So `array` is the base address, and `sizeof(TYPE)` * `x` is the offset. If `x` happens to be 0, you end up with your first element. And I guess that's also why arrays tend to start with 0.

[^1]: I know that there are other ways so that you don't have to know the number beforehand, this is to keep it simple.