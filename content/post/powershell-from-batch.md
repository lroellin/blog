+++
title = "Start Powershell script from Batch"
date = 2014-07-01T03:42:55+02:00
+++

Today, I'll share a little code snippet with you that I use everyday:

```dos
@echo off
set script="ScriptsScript.ps1"

powershell.exe -NoProfile -File "%script%"
```

Since Powershell scripts don't open right away when you click on them (for various reasons that are too long to discuss here, but make sense), this re-enables that feature with a workaround.