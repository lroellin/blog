+++
title = "Ever heard of an ifdowhile-Loop?"
date = 2014-07-15T03:51:16+02:00
+++

I hope you didn't...

OpenSSL-cleanup project LibreSSL has a [commit](http://opensslrampage.org/post/91570897957/never-heard-of-an-ifdowhileloop-before) fixing an `ifdowhile` loop into a simple `while` loop. Wait, what?

This piece of code has made it into one of the most used crypto libraries:

```cpp
if (*p == '\0')
do {
	if (RAND_bytes(p, 1) <= 0)
	return 0;
} while (*p == '\0');
```

# Programming in C: Lesson 1

This makes no sense at all. According to K&R:

> while (expression)
> statement
> The expression is evaluated. If it is non-zero, statement is executed and expression is reevaluated. This cycle continues until expression becomes zero, at which point execution resumes after statement.

... which basically means "it'll do what you told it, as long as expression is true". The `while` statement is a pre-test-loop which means that it tests first, then runs the code. If the test fails on the first run, the code won't run.

Then there's the `do-while` loop. Let's get back to praised K&R:

> do
> statement
> while (expression);
> The statement is executed, then expression is evaluated. If it is true, statement is evaluated again, and so on. When the expression becomes false, the loop terminates.

... which means about the same, except this is a post-test-loop. This means the code will run at least once, even if the test will fail afterwards; it stops then. (There are `for` loops to consider as well, but they're more for counting or iterating).

I think someone got these two concepts a bit wrong and ended up mixing them together. This is like saying:
If the washing machine is running
then wait another minute until checking again
repeat only if the washing machine is running

Which any sane person would shorten to:
While the washing machine is running
then wait another minute until checking again
# Conclusion & Fix
~~I am not sure if this is some low-level thing that makes sense in any way (like using goto in the Linux kernel for readability reasons), but I don't get it. How can a programmer that has not just started learning C come up with this kind of code?~~

**Update next day**: after thinking about it some time (remember [taking a step back]({{< relref "post/take-a-step-back.md" >}})) I've come to the conclusion that the developer simply did not know or forgot about the pre-test `while`. He knew that there is a way to repeat something as long as there is a condition given, but did not know how to make the entry point, so he combined `if` and `do-while`.

Does anyone know if this was the right way to do some time ago? So that a `while` loop is essentially syntactic sugar, like the `for` loop can be broken down into a `while` loop and a set of `switch` cases into `if-elseif`?

Fortunately, LibreSSL corrected this to:

```cpp
while (*p == '\0') {
	if (RAND_bytes(p, 1) <= 0)
	return 0;
}
```
