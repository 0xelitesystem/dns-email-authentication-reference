# DMARC

DMARC ties SPF and DKIM together: it is a DNS record that tells receiving servers what to do with mail claiming to be from your domain that fails authentication, and it sends you reports about that mail. It is what turns SPF and DKIM from checks into an enforceable policy.

## What DMARC adds

SPF and DKIM let receivers check authentication, but on their own they do not tell receivers what to do with mail that fails, nor do they report back to you. DMARC fills both gaps. It publishes a policy instructing receivers to deliver, quarantine, or reject mail that fails authentication and is not aligned with your domain, and it requests reports so you can see what mail is being sent in your domain's name. DMARC is the policy and visibility layer on top of SPF and DKIM.

## The policy options

A DMARC policy can tell receivers to take no special action on failing mail (`p=none`), to treat it with suspicion such as sending it to spam (`p=quarantine`), or to reject it outright (`p=reject`). The strictest policy, reject, means mail failing authentication in your domain's name is not delivered at all, which is the strongest protection against spoofing. The policy is yours to set, and the goal over time is usually to reach an enforcing policy once you are confident your legitimate mail all passes. The policy is how DMARC actually stops spoofed mail rather than just observing it.

A typical starting record, published as a TXT record at `_dmarc.yourdomain.com`:

```
v=DMARC1; p=none; rua=mailto:dmarc-reports@yourdomain.com
```

`p=none` observes and reports without affecting delivery; `rua=` is where aggregate reports go. After a monitoring period confirms all legitimate mail passes, tighten to `p=quarantine` and then `p=reject`.

## The reports

DMARC requests that receivers send you reports about mail claiming to be from your domain, including what passed and failed authentication. These reports are valuable: they reveal every source sending mail in your domain's name, legitimate ones you may have forgotten and illegitimate ones spoofing you. Reading the reports before enforcing a strict policy is how you confirm all your real mail passes, so that enforcement blocks spoofers without blocking yourself. The reports are the safety mechanism for rolling out enforcement.

## Alignment

DMARC checks not just that SPF or DKIM passed, but that the passing authentication aligns with the domain in the visible from address. This alignment requirement is what makes DMARC effective against spoofing, because it ties the authentication to the address the recipient actually sees. Mail can pass SPF or DKIM for some other domain yet still fail DMARC if it does not align with the from address it is claiming. Alignment is the detail that closes the gap a spoofer would otherwise exploit, and it is central to how DMARC protects the address recipients trust.
