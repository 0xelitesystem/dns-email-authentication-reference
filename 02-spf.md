# SPF

SPF, the Sender Policy Framework, is a DNS record that lists which mail servers are authorized to send email for your domain. Receiving servers check whether a message came from a listed server, which helps detect mail forged to appear as if it is from you.

## What SPF declares

An SPF record published in your domain's DNS names the servers and services permitted to send mail on behalf of your domain. When a receiving server gets a message claiming to be from your domain, it can check the SPF record to see whether the sending server is on the authorized list. Mail from an authorized server passes the SPF check; mail from an unlisted server does not. SPF is essentially your published list of legitimate senders.

A typical record, published as a TXT record on the root of your domain:

```
v=spf1 include:_spf.google.com include:mailgun.org ~all
```

Each `include:` pulls in a provider's authorized servers. The ending matters: `~all` is a soft fail (unlisted senders are marked suspicious but usually still delivered), while `-all` is a hard fail (receivers are told to reject them outright). Start with `~all` while you confirm every legitimate sender is listed, then move to `-all`. One domain gets exactly one SPF record, and the spec allows at most 10 DNS lookups, so too many `include:` entries silently breaks it.

## Why it helps

SPF helps detect spoofing because forged mail usually originates from servers not on your authorized list, so it fails the SPF check. A receiver seeing an SPF failure has a signal that the mail may not be genuine. SPF also supports your legitimate mail by confirming, for receivers, that your real sending servers are authorized. It is the first layer: establishing which servers are allowed to send as you.

## Include every sender

A common SPF mistake is forgetting to include all the services that legitimately send mail for your domain: your mail provider, but also any newsletter platform, support system, or other service that sends on your behalf. Each must be in the SPF record, or its mail will fail SPF. Inventorying everything that sends as you, and listing all of it, is essential. An incomplete SPF record causes your own legitimate mail to fail, which is worse than the spoofing it was meant to stop.

## SPF has limits

SPF alone has limits: it checks the sending server but not the message contents, and it can break when mail is forwarded, since forwarding changes the sending server. These limits are why SPF is paired with DKIM and DMARC rather than used alone. SPF establishes authorized servers; DKIM verifies the message itself; DMARC reconciles them and handles the forwarding and policy questions SPF cannot. SPF is necessary but not sufficient on its own, which is the reason the other two exist.
