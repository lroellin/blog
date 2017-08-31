+++
title = "Logitech mouse: Thumb buttons don't hold"
date = 2014-06-27T03:41:34+02:00
+++

After reinstalling Windows, I ran into the same problem as when I just bought my mouse: when assigning the thumb buttons (usually forward/backward in the web browser) to moves like "Crouch (hold)", it did not hold. Instead, just one key stroke was sent, so you had to set it to "Crouch (shift)".

The problem is, that these buttons have a special assignment in SetPoint. Instead of just plain thumb buttons, SetPoint interferes your "clicks" and sends just one key stroke. The problematic assignment is "Web Forward"/"Web Backward".

To get rid of this and have a proper, normal behaviour, choose "Generic" or "Other: Generic".

Source: http://forum.ventrilo.com/showthread.php?t=41451, posted here because I'll forget it the next time and it's easier to find when you just describe your symptoms.