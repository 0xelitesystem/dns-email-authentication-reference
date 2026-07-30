# DNS Email Authentication

A plain-language reference on SPF, DKIM, and DMARC: the three DNS records that prove your email is really from you, stop others from spoofing your domain, and keep your messages out of spam. It covers what each one does, how they work together, and a sensible order to set them up. Written for operators who send email from their own domain.

## The core idea

SPF, DKIM, and DMARC are records you publish in your domain's DNS that let receiving mail servers verify your email is authentic. SPF says which servers may send for your domain; DKIM cryptographically signs your messages; DMARC ties the two together and tells receivers what to do with mail that fails. Together they prove your mail is really yours, block spoofing of your domain, and improve whether your legitimate mail reaches inboxes.

## What is inside

- [01-why-it-matters.md](01-why-it-matters.md) spoofing, deliverability, and trust.
- [02-spf.md](02-spf.md) authorizing your sending servers.
- [03-dkim.md](03-dkim.md) signing your messages.
- [04-dmarc.md](04-dmarc.md) tying it together and setting policy.
- [05-setup-order.md](05-setup-order.md) a sensible order and rollout.

## The stance

This reference treats email authentication as essential for anyone sending from their own domain: without it, your mail is more likely to be spam-filtered and your domain is open to being spoofed. It favors a careful rollout, especially for DMARC, to avoid blocking your own legitimate mail.

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## License

MIT. Copyright 0xelitesystem 2026.
