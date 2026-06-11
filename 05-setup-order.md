# Setup order

Set up SPF first, then DKIM, then DMARC, and roll out DMARC gradually, starting with a monitoring policy and reading the reports before tightening to enforcement. This order lets each layer build on the last and prevents DMARC from blocking your own legitimate mail.

## SPF and DKIM first

Begin with SPF and DKIM, because DMARC depends on them. Publish an SPF record listing every service that sends mail for your domain, and enable DKIM signing on each of those services with their public keys published in DNS. Get these working and verify that your legitimate mail passes both. DMARC enforcement only makes sense once SPF and DKIM are correctly covering all your real mail, so they come first.

## DMARC in monitoring mode

Once SPF and DKIM are in place, publish a DMARC record in its monitoring policy, the one that takes no action on failing mail but requests reports. This lets you observe what mail is being sent in your domain's name without risking any legitimate mail. The monitoring phase is for discovery: finding every legitimate sender, confirming they all pass, and spotting any spoofing, all before you turn on enforcement that would actually block mail.

## Read the reports, then tighten

Read the DMARC reports through the monitoring phase until you are confident that all your legitimate mail passes authentication and aligns. The reports will reveal any sender you missed in SPF or DKIM, which you then fix. Only once everything legitimate passes do you tighten the policy, typically stepping from monitoring to suspicion to full rejection. This gradual tightening, guided by the reports, reaches strong enforcement without ever blocking your own mail. Patience here is what prevents the classic mistake.

## The mistake to avoid

The mistake to avoid is jumping straight to a strict, enforcing DMARC policy before confirming all your legitimate mail passes. Do that and you may block your own mail, sending real messages to rejection while you scramble to find what failed. The whole point of the monitoring phase and the reports is to prevent this. Build up the layers in order, watch the reports, and enforce only when the evidence says it is safe. The careful rollout is slower but avoids the painful and visible failure of blocking yourself.
