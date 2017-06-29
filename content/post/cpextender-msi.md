+++
title = "CPExtender.msi"
date = 2015-03-18T14:37:56+02:00
+++

A customer needed the MSI for the SSL Network Extender. Searching through documentation, I was told that this *should* be in in

    $FWDIR/conf/extender

which is not true. It's **actually** in

    $FWDIR/conf/extender/CSHELL.

There is the package you need, a .cab and an already extracted .msi.

If you don't know how to get the file from there: set one user's shell to Bash. Then use WinSCP with that user's credentials.