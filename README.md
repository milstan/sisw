# 1st Self-Improving Software Workshop
San Francisco, California

The coding capabilities of frontier models make us all wonder what is the future of Software Engineering. 

We believe **"The best way to predict the future is to create it"** (Dennis Gabor).

We're seeing the first signs of software being able to self-improve, and are curious to push the boundaries of self-improving software and see where it takes us. 

We also believe several minds are smarter than one.

So we're organising this gathering of like-minded (call us crazy) people trying to make software self-improving — to share what we tried, discovered, what seems to be working, and what doesn't. 

**No titles, no degrees, just learnings.**

We invite submissions of **5-minute talks** (including Q&A - nothing fancy - just present what you're doing) and mingle. Ideally share a GitHub asset (a skill, a repo, even just a report of what you've observed).

> **When:** May 21, 2026 · 6pm PDT
> **Where:** San Francisco, California · Parrot office

**Organizers:** [Milan Stankovic](https://github.com/milstan) ([Leadbay](https://leadbay.ai)) & [Erik Dahl](https://github.com/erikd234) ([Parrot](https://parrotapp.com))

[**→ Submit your talk**](https://github.com/milstan/sisw/issues/new?template=talk-submission.yml)

[RSVP on Luma](https://luma.com/lkni43xl)

---

## Who's coming

<!-- TALKS:START -->
| Speaker | Talk |
|---|---|
| [**Milan Stankovic**](https://github.com/milstan)<br>[leadbay.ai](https://leadbay.ai) · [𝕏](https://x.com/milstan) · [🔗](https://gist.github.com/milstan/3b12f938f344f4ae1f511dd19e56adce) | A coding agent using a thinking frontier model can iterate overnight and deliver a perfected software output with very limited instructions. It seems to work best when the agent can perform a qualitative assessment of the work, and score it on some scale that becomes a reward function the agent optimizes through iterations (like gradient descent). |
| [**Erik Dahl**](https://github.com/erikd234)<br>[parrotapp.com](https://parrotapp.com) | The thesis  A lot of devs right now are getting good at running 5–10 parallel Claudes — checking in on each one, unsticking it, answering its questions, ferrying context between them. […](https://github.com/milstan/sisw/issues/12) |
| [**Mehul Agarwal**](https://github.com/agarwalml)<br>[koyal.ai](https://koyal.ai) · [𝕏](https://x.com/meh_agarwal) | Domain specific agentic harnesses  Claude Code / Codex works out of the box for software, but most businesses aren’t software businesses. […](https://github.com/milstan/sisw/issues/14) |
| [**Rakesh Mehta**](https://github.com/rakeshvmehta)<br>[zarnaai.com](https://zarnaai.com) · [𝕏](https://x.com/rak3sh_m) | Recently, there has been a lot of buzz about building a software factory and tokenmaxxing, but the variance in results for people who have tried to implement this for production-grade software has been very mixed. […](https://github.com/milstan/sisw/issues/16) |
| [**Dhruv Roongta**](https://github.com/Dhruv317)<br>[slashy.com](https://slashy.com) · [𝕏](https://x.com/DhruvRoongta) | We're building an AI-native email client that helps draft emails in the user's voice, triage emails, and never drop the ball on emails. […](https://github.com/milstan/sisw/issues/18) |
| [**pranav bedi**](https://github.com/pranavbedi)<br>[moda.dev](https://moda.dev) · [𝕏](https://x.com/pranavbedi) | Agents today learn like 2010-era SaaS: a human watches a dashboard, files a ticket, opens a PR. The user is upstream of the fix by days. That's backwards, the user interaction IS the training signal. Every frustration, abandonment, and silent failure is a labeled example of what the agent shouldn't have done. The job is to extract those labels automatically and pipe them into the next self-edit cycle.  Example: one user typed "i received nothing, how come" at 2am. |
| [**Tiger Wang**](https://github.com/thenewpotato)<br>[nessielabs.com](https://nessielabs.com) · [𝕏](https://x.com/tigerjwang) · [🔗](https://github.com/nessielabs/boring-orchestrator) | The path to self-improving software is easier (and more agentic) than you might think. Our internal agent platform runs on ~500 lines of Express + SQLite + cron calling `claude -p` — no agent framework, no multi-agent protocol, no message bus. It's been running PR reviews and user-facing email campaign agents across Nessie in production. I'll share why we haven't needed anything fancier, where the simple loop actually breaks, and the case for under-engineering your orchestrator in 2026. |
| [**Shashank Agarwal**](https://github.com/imshashank)<br>[noveum.ai](https://noveum.ai) · [𝕏](https://x.com/itsshashank) | AI agents are already silently failing in production — most enterprises just don’t realize it yet. […](https://github.com/milstan/sisw/issues/24) |
| [**Alexandru Turcanu**](https://github.com/pondorasti)<br>[flaco.851.sh](https://flaco.851.sh) · [𝕏](https://x.com/pondorasti) | Making AI multiplayer.  Every company wants a self improving AI Agent like [River](https://x.com/tobi/status/2053121182044451016) or [Inspect](https://builders.ramp.com/post/why-we-built-our-background-agent), yet existing harnesses like OpenClaw quickly fall apart the moment you add them in Slack.  We’ll explore how we built an agent harness for teams and dive into the details that power it: - thread isolation with sandboxing - shared memory model - capabilities that go beyond MCPs |
| [**Saai Arora**](https://github.com/Saai151)<br>[tryreplicas.com](https://tryreplicas.com) · [𝕏](https://x.com/saaiarora) | We're building replicas which is a cloud coding agent where you bring your own credentials for Claude Code or Codex. Customers like Mintlify and Composio use us to do everything from writing code to E2E testing via automations and integrations with Slack and Linear. Each agent works inside customizable VM environments, so work is parallelized and shareable across the team. Replicas can access sources like databases, Datadog or Notion, and return screenshots and videos as proof of work. |
<!-- TALKS:END -->

<!--
The "Who's coming" block is auto-regenerated from _data/talks.yml by
.github/workflows/submission-to-pr.yml on every merge. Don't hand-edit
between the TALKS:START and TALKS:END markers.

Organizer notes (submission flow, dedup, RSVP setup, file map): see
ORGANIZING.md.
-->
