# Security policy

This repository is part of [Yoraito Labs](https://yoraito.ai/labs). It is alpha software
that handles financial data, so please treat it that way.

## Supported versions

Only the latest release and the `main` branch receive fixes. Older alpha builds are not
supported.

## Reporting a vulnerability

Email **security@yoraito.ai**. Do not open a public issue.

Please include:

- the affected version, tag or commit;
- the operating system and how you installed it;
- steps to reproduce, with a clear impact statement;
- a proof of concept if you have one.

Redact real financial data. Use synthetic samples or a demo company. Do not test against
accounts, ledgers or banks you do not own or have written permission to use.

We acknowledge within 3 business days and aim to give an initial assessment within 10.
We will tell you when a fix is ready and credit you if you want credit.

## Scope

In scope:

- the desktop app and its installer;
- the local web UI and the local API on 127.0.0.1;
- connectors, OAuth flows and token storage;
- the audit log and the evidence trail;
- packaging scripts and update paths;
- the hosted token exchange where this repository contains it.

Out of scope:

- findings in third-party services or accounting systems (report those to the vendor);
- social engineering, phishing and physical access;
- denial of service and volumetric attacks;
- issues that require a already-compromised machine or stolen credentials.

## Safe harbour

We will not pursue legal action for good-faith research that follows this policy, stays
within the scope above, and does not access, modify or exfiltrate other people's data.
If you are unsure, email us before you test.

## No bounty

There is no paid bounty programme at this stage.

## Hosted keys

Never share a Yoraito-hosted key. If one leaks, email security@yoraito.ai so we can revoke
it.
