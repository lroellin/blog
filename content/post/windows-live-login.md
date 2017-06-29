+++
title = "Windows Live/Microsoft Account: DomainUser Format"
date = 2014-02-09T01:17:25+02:00
+++

Since Windows 8, you can log in to your PC using your Windows Live credentials. However, since this is not a local account anymore, `.username` won't work anymore.

If this format is needed, (e.g. RDP login), use:

    MicrosoftAccount\windowslive_account</em>

So if you registered with "you@bluewin.ch", this would be

    MicrosoftAccount\you@bluewin.ch

PS: Yes. you can use your normal E-mail address instead of @hotmail or @outlook, at least that worked 10 year ago

PPS: I'm feeling old now...