+++
title = "Spring/Hibernate @Transactional pitfall"
date = 2017-04-29T16:29:40+02:00
+++

We're currently doing a student project which I hope to show off in the future. EDIT: it's about https://teiler.io. However, yesterday I ran into a problem where I want to document the fix.

We have a repository method that is marked as `@Transactional` to delete a certain row. At first, we called that in a loop, from a method from one of our `@Service` classes and it worked fine. 

We then refactored it and added a method to the repository, which accepts a list and then does the looping for us, calling the other repository method in the loop. Then stuff broke. 

We got a lot of the following messages:

> org.springframework.dao.InvalidDataAccessApiUsageException: No EntityManager with actual transaction available for current thread - cannot reliably process 'remove' call

The part "No EntityManager with actual transaction available for current thread" points to a transaction problem, which happens when you don't use `@Transactional`. But we did. So what happens? 

Remember that annotations are worked out by using reflection. And reflection is, sometimes, a bit magic. And here it failed. 

The problem was, that the `@Transactional` on the actual remove method wasn't picked up, when it was called from another method in the repository. So no transaction was started. 

To fix this, you have to add `@Transactional` to the method you call from outside your class - the one that accepted the list. That fixed the problem! 