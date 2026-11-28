# COAE — AI Red Teaming Notes

My notes from the **Hack The Box Academy AI Red Teamer** path: how machine learning works, the attack surface it creates, and which payloads and defenses actually hold up in the labs.

This is an [Obsidian](https://obsidian.md) vault. Notes read fine on GitHub, but `[[wikilinks]]` and image embeds only resolve when the folder is opened as a vault.

## Modules

| # | Module | Covers |
|---|---|---|
| 1 | [Fundamentals of AI](1.%20Fundamentals%20of%20AI) | Regression, decision trees, naive Bayes, SVMs, and the data assumptions each one makes |
| 2 | [Applications of AI in InfoSec](2.%20Applications%20of%20AI%20in%20InfoSec) | Environment setup, scikit-learn and PyTorch, and an end-to-end spam classifier |
| 3 | [Intro to Red Teaming AI](3.%20Intro%20to%20Red%20Teaming%20AI) | Red teaming vs. vulnerability assessment, plus the ML OWASP Top 10 (ML01–ML10) |
| 4 | [Prompt Injection Attacks](4.%20Prompt%20Injection%20Attacks) | Recon and fingerprinting, system prompt leaking, indirect injection, jailbreaking, `garak`, and mitigations |
| 5 | [LLM Output Attacks](5.%20LLM%20Output%20Attacks) | Treating model output as untrusted: XSS, SQL and code injection, markdown exfiltration, function calling |
| 11 | [AI Privacy](11.%20AI%20Privacy) | Membership inference, model inversion, model theft, and differential privacy as the countermeasure |

[MATH REFRESHER.MD](MATH%20REFRESHER.MD) is a notation lookup for module 1.

## Recurring themes

- A model receives the system prompt and the user prompt as one stream of text. There is no boundary between instructions and data — that single fact is what makes prompt injection possible.
- Model output is untrusted input to whatever consumes it next: the browser, the shell, the database.
- Any defense that depends on the model choosing to behave is not a defense.

## Scope

Everything here was run against Hack The Box lab targets built to be attacked. Nothing in this repo is for use against systems you don't have written permission to test.
