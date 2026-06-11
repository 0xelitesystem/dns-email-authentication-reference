# DKIM

DKIM, DomainKeys Identified Mail, adds a cryptographic signature to your outgoing messages, and publishes the matching key in your DNS, so receiving servers can verify that a message genuinely came from your domain and was not altered in transit.

## What DKIM does

DKIM signs each outgoing message with a cryptographic key, and you publish the corresponding public key in your domain's DNS. A receiving server uses the published key to verify the signature, confirming two things: the message really came from your domain, and it was not changed after signing. This is a stronger verification than SPF, because it ties the message itself, not just the sending server, to your domain. DKIM proves message authenticity, not just server authorization.

## Why it is stronger

Because DKIM verifies the message content through a signature, it survives some situations that break SPF, such as forwarding, where the sending server changes but the signature travels with the message. It also detects tampering, since any alteration breaks the signature. This makes DKIM a strong check on whether a message is genuinely your unaltered mail. Where SPF asks whether the server is authorized, DKIM asks whether the message is authentic, which is a deeper question.

## Key management

DKIM relies on a key pair: a private key your mail system uses to sign, and a public key published in DNS for verification. The private key must be kept secure, since anyone with it could sign mail as you. Keys are rotated periodically as good practice, replacing the published key with a fresh one. Managing these keys, keeping the private one safe and the public one correctly published, is the ongoing maintenance DKIM requires. Most mail providers handle the mechanics, but the keys are the heart of it.

## Set it up through your provider

In practice, DKIM is usually configured through your mail provider or sending service, which generates the keys and gives you the DNS record to publish. Each service that sends mail for you may have its own DKIM setup. Following each provider's instructions to enable signing and publish the matching DNS record is how DKIM gets deployed. As with SPF, every service that sends as you should be signing its mail with DKIM, so the verification covers all your legitimate mail, not just some of it.
