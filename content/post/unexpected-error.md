+++
title = "The problem with \"Unexpected error\""
date = 2013-12-19T00:40:00+02:00
+++

You may have seen applications that crash weirdly. What's the message?

![](/post/vs-unexpectederror.png)

> What?! An *un*-expected error? What error is expected anyway?!

Ok, this is another one of those messages, that is technically correct, but makes no sense from a user's perspective.

This is connected to the definition of an error:

* User: something has completely gone wrong
* Technician: something has not gone the way the machine was instructed to (*but* may have worked anyway)

So this message means:

* User: BOOO, the application has bugs and even expects them. How BAD is that?!
* Technician: We haven't catched that error yet

Wait, waddaya mean *catch* an error? Like in Pokemon? Oh I'm so gonna do software development for a living!

![](/post/pokemon.jpg)

Uhm... let's go deeper into where this message originates:

From a technical perspective, you often use the try-catch-finally pattern. That means:

* **Try** something that may lead to a few errors you already know about - these may be not critical (e.g. delete a file)
* **Catch** expected errors (e.g. file not found, where this may have been deleted before and you don't need it anyway)</li>
* **Catch** unexpected errors in a controlled manner
* *Optional* **Finally** do something in every case, even if the error is so critical, that the application has to quit (e.g. closing a file handle)

Below is a Powershell example of that. The optional finally-part is not used:

```powershell
Try
{
    # This may not exist, we just don't want it here
    Remove-Item "C:somenonexistentfolderfile.txt" -ErrorAction Stop
}

Catch [System.Management.Automation.ItemNotFoundException]
{
    # No problem, skip it silently
    Write-Debug "Item not found"
}

Catch
{
    # Ok, something bad went wrong!
    # WRONG
    Write-Host "Unexpected error"

    # RIGHT (at least not misleading)
    Write-Host "Sorry, something went wrong. Please call your system administrator."
    Write-Debug "Error: $($error[0])"
}
```

Source: http://stackoverflow.com/questions/6779186/powershell-try-catch-finally

*Side note: You only see the Write-Debug messages, when you want them (as a technician). Unfortunately, I have not found a way to redirect them to a file, but this is not the scope of this post.*

What should you do then? Simply show a message that AN error has occurred, and write that error to a debug log file. For expected errors, skip the message and simply write it to a log file.

You see, that this is all about wording. Why a full blog post for that issue? People seem still not to get it, that Everyday Joe has no idea of try-catch-finally (and does not need to have). But he will react that way and blame your application.

Just be nice and forgiving to your users, lead them through your app. NEVER shout at them and don't use technical terms.