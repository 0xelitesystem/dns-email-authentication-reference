# Why it matters

Email authentication matters because without it, anyone can send email that appears to come from your domain, and receiving servers are more likely to treat your legitimate mail as spam. SPF, DKIM, and DMARC prove your mail is genuinely yours, which protects your domain from spoofing and your messages from the spam folder.

## The spoofing problem

Email was not built with sender verification, so by default the from address on a message can be forged. Without authentication, anyone can send mail that appears to come from your domain, which enables impersonation, phishing in your name, and damage to your reputation. Authentication records close this by letting receivers verify that mail claiming to be from your domain actually is. They turn an unverifiable claim into a checkable fact.

## The deliverability problem

Receiving mail servers use authentication as a signal of legitimacy when deciding whether to deliver mail to the inbox, the spam folder, or not at all. Mail from a domain with proper authentication is more likely to be trusted and delivered; mail without it is more likely to be filtered or rejected. For anyone who sends important email from their own domain, missing authentication means legitimate messages quietly landing in spam. Authentication is now effectively required for reliable delivery.

## Protecting your domain and recipients

Authentication protects two parties at once. It protects your recipients from being deceived by mail forged to look like it came from you, since spoofed mail can be detected and stopped. And it protects your domain's reputation, because spoofing in your name harms how your domain is perceived. By proving which mail is really yours, authentication defends both the people you correspond with and the standing of your domain itself.

## The three work together

SPF, DKIM, and DMARC are not alternatives; they work together, each covering part of the problem. SPF authorizes sending servers, DKIM verifies the message was not altered and came from your domain, and DMARC ties these together and tells receivers what to do when checks fail, plus reports back to you. Deploying all three gives complete coverage; deploying only some leaves gaps. The following sections cover each in turn, then how to roll them out.
