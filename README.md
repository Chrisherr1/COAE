# COAE — AI Red Teaming Notes

My working notes from the **Hack The Box Academy AI Red Teamer** path: the theory behind machine learning, the attack surface it creates, and the payloads and defenses that actually hold up in the labs.

This is an [Obsidian](https://obsidian.md) vault, so notes use `[[wikilinks]]` and `![[image]]` embeds. Everything renders fine on GitHub, but internal links and image embeds only resolve when the folder is opened as a vault.

---

## Modules

| # | Module | What's in it |
|---|---|---|
| 1 | [Fundamentals of AI](1.%20Fundamentals%20of%20AI) | ML vs. deep learning, linear and logistic regression, OLS, decision trees (entropy, information gain), naive Bayes, SVMs, and the data assumptions each one makes |
| 2 | [Applications of AI in InfoSec](2.%20Applications%20of%20AI%20in%20InfoSec) | Environment setup (Miniconda, JupyterLab), scikit-learn and PyTorch, and an end-to-end spam classifier — preprocessing, tokenizing, stop words, stemming, feature extraction |
| 3 | [Intro to Red Teaming AI](3.%20Intro%20to%20Red%20Teaming%20AI) | Red team vs. vulnerability assessment for ML systems, and the full **ML OWASP Top 10** (ML01–ML10) with notes and source papers per entry |
| 4 | [Prompt Injection Attacks](4.%20Prompt%20Injection%20Attacks) | Recon and fingerprinting, system prompt leaking, indirect injection, jailbreaking, scanning tools, and mitigations — see below |

**Reference:** [MATH REFRESHER.MD](MATH%20REFRESHER.MD) — notation lookup for module 1. Grandfathered in; it predates the note rules.

---

## Module 4: Prompt Injection Attacks

The most built-out section, since it's where most of the practical work lives.

| Note | Covers |
|---|---|
| [1. Prompt Injection & Sensitive Disclosure](4.%20Prompt%20Injection%20Attacks/1.%20Prompt%20Injection%20%26%20Sensitive%20disclosure..md) | OWASP LLM Top 10 #1 and #2. Reconnaissance, identifying which layer enforces a refusal (input filter, output filter, or training), LLMmap fingerprinting, and seven strategies for leaking a system prompt |
| [2. Indirect Prompt Injection](4.%20Prompt%20Injection%20Attacks/2.%20Indirect%20Prompt%20Injection.md) | Attacking through ingested data instead of the chat box — false positives against other users, HTML-comment payloads in summarized pages, and SMTP injection via `swaks` |
| [3. Jailbreaking](4.%20Prompt%20Injection%20Attacks/3.%20Jailbreaking.md) | DAN, role-play, fictional scenarios, token smuggling, adversarial suffixes, Opposite/Sudo mode, and Infinitely Many Meanings |
| [4. Tools to Help Secure AI](4.%20Prompt%20Injection%20Attacks/4.%20Tools%20to%20Help%20Secure%20AI.md) | `garak` LLM vulnerability scanning — probes, detectors, reports — plus ART and PyRIT |
| [5. Prompt Injection Mitigations](4.%20Prompt%20Injection%20Attacks/5.%20Prompt%20Injection%20Mitigations.md) | Why prompt engineering and blacklists fail, and what works instead: least privilege, human in the loop, fine-tuning, adversarial prompt training, guardrail LLMs |

### Takeaways

- An LLM receives the system prompt and the user prompt as one stream of text. There is no boundary between instructions and data — that single fact is what makes this whole attack class possible.
- LLMs are non-deterministic. A payload that fails now can land on the 5th or 10th try, and a fresh session often matters more than a better prompt.
- Any defense that depends on the model choosing to behave is a defense you can't rely on.
- As long as a user can reach the model, it's exploitable — directly or indirectly.

---

## Scope

Notes from a training environment. Every payload and command here was run against Hack The Box lab targets built to be attacked. Nothing in this repo is for use against systems you don't have written permission to test.
