---
kind: "article"
created_at: "2014-04-15 28:36:17 +04:00"
title: "outlook.com + custom domains + activesync (solved)"
tags: [ 'outlook.com', 'activesync', 'android' ]
---
If you got here, then you have already seen the text below.

> Exchange ActiveSync (EAS) settings for Outlook 2013 with Microsoft CUSTOM Live Domains / Outlook.com account 
> 
> If anyone can make this work, or find the person at Microsoft responsible for randomly setting EAS server names for Outlook.com accounts and Microsoft live custom domains (see http://domains.live.com), then they would be a god. I have been trying to find a solution to this for 6 months, and have spent about 80 hours talking to friendly but incompetent Microsoft Support People in the departments of, Microsoft Accounts, Outlook.com Accounts, Office 365, Exchange Server Support (because all other personnel transfer me there because they don't understand how email works).
> 
> I have tried the following servers names to setup Exchange ActiveSync (EAS) to connect with my live custom domains (see http://domains.live.com) to the Outlook 2013 email client.
> 
> I am able to use EAS with a @outlook.com, @live.com, and @hotmail.com email address, by using "s.outlook.com" as a servername (by the way, I just found that today after 6 months and discussions with about 100 MS employees)
> 
> However, "s.outlook.com" doesn't work with live custom domains (which, it is unclear who manages their MX servers, outlook.com or some old live.com system)
> 
> I have also tried the following names:
> "blu-m.hotmail.com"
> "www.outlook.com"
> "m.hotmail.com"
> "s.outlook.com"
> "snt-m.hotmail.com"
> 
> No luck.
> 
> And, I am 99.9999999% certain that of the 1000 times I typed in the password, I got it correct at least once.
> 
> I am not the only one who has been trying to find a solution to this problem, nor have I been trying the longest. I have found blogs, forums, and even threads here that are over a year old and have no solution, or people claim to have a solution that worked for them, but it no longer works.
> 
> What is the deal. You would think that Outlook 2013 should automatically setup any Microsoft related service automatically. All the other programs, excel, word, etc work seemlessly through skydrive to sync all settings based on Windows login credentials. Why is Outlook.com and Outlook 2013 have so much difficulty with this. Email is the oldest thing in the book to sync.
> 
> Here are other threads that have either not found a solution, or some claim to have found solutions that clearly don't work for others:
> 
> The official documentation, that claims s.outlook.com is the solution for
> "Apps that support Exchange ActiveSync", which I assume would include Outlook 2013, but apparently not. 
> 
> Also, you would think the correct instructions would be under
> "Microsoft Office -> Get info on setting up Outlook.com in Microsoft Office Outlook here." But, that makes you believe it will work automatically, which would be the ideal behavior, but it doesn't work with Microsoft live custom domains. 
> 
> Here they give: "m.outlook.com", and use a custom domain as an example:
> http://help.outlook.com/en-Us/140/bb896613.aspx
> That doesn't work either.
> 
> here I am. Still no solution after a total of 6 months searching, and an unused Outlook 2013, which I paid for.
> 
> Hopefully, this highlights how absurd it is that Microsoft hasn't just given out the Exchange ActiveSync settings for Outlook.com Custom Domains that will work with Outlook 2013.
> 
> Anyone? I personality know 3 IT colleagues who had the same problem (They don't anymore, they gave up and instead use IMAP with gmail's custom domains.) If I know 3, then how many other silent IT guys are out there?

The solution is simple, you need to create alias. Outlook.com -> Options -> Create an Outlook.com alias. Next you need to use this alias as login instead you@domain.com . That's all.
