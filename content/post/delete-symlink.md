+++
date = "2013-10-04T22:03:44+02:00"
title = "Delete symlink"
+++

To delete a symlink (only the link), you treat it like a file.

However, if you try this, you get:
("r" is my symlink)

```bash
rm r/
rm: cannot remove `r/': Is a directory
```

Ok, if rm is of no help, rmdir should, as it (sort of) tells me

```bash
rmdir r/
rmdir: failed to remove `r/': Not a directory
```

Uh-oh.

I then went on the Internet (Top Gear reference intended) and found out, what the problem was:
The / (slash) on "r/"

```bash
rm r
```

went just fine :)

Well, where did it come from? Tab completion.

Lesson learned: Tab completion is only 99.8% right. Where has that other .1% gone? Safety margin.