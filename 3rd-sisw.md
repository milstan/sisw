# 3rd Self-Improving Software Workshop
San Francisco, California · September 3, 2026

The coding capabilities of frontier models make us all wonder what is the future of Software Engineering.

We believe **"The best way to predict the future is to create it"** (Dennis Gabor).

We're seeing the first signs of software being able to self-improve, and are curious to push the boundaries of self-improving software and see where it takes us.

We also believe several minds are smarter than one.

So we organised this gathering of like-minded (call us crazy) people trying to make software self-improving — to share what we tried, discovered, what seems to be working, and what doesn't.

**No titles, no degrees, just learnings.**

We invited submissions of **5-minute talks** (including Q&A - nothing fancy - just present what you're doing) and mingle. Ideally share a GitHub asset (a skill, a repo, even just a report of what you've observed).

> **When:** September 3, 2026 · 6pm PDT
> **Where:** San Francisco, California · [Moda office](https://moda.dev/)

**Organizers:** [Milan Stankovic](https://github.com/milstan) ([Leadbay](https://leadbay.ai)) & [Erik Dahl](https://github.com/erikd234) ([Parrot](https://parrotapp.com))

👉 **Looking for the next edition?** See the [4th SISW announcement](README.md). Previous editions: [1st SISW](1st-sisw.md) · [2nd SISW](2nd-sisw.md).

---

## Talks

| Speaker | Talk |
|---|---|
| [**John Oram**](https://github.com/joram)<br>[www.veiilstream.com](https://www.veiilstream.com) | > As implementation effort falls, specification and verification absorb more of the engineering effort.  This talk compares the software development process when software is primarily built by human developers versus when software can increasingly observe, modify, test, and improve itself.  The goal is not to argue that engineering effort disappears. The goal is to show how that effort shifts. |
| [**Videh Seksaria**](https://github.com/videh-mnemonic)<br>[mnemoniclabs.ai](https://mnemoniclabs.ai) | We've built personal AI models for ourselves which learn how we steer coding agents. These personal models learn our taste, judgement, and thought process better than context / prompt engineering. We use these models to steer an underlying gpt/claude model giving us personalization + frontier generation.  Given this is a 5-minute talk, I plan to start with a demo of the experience and then quickly cover how we trained these models. |
| [**Tiger Wang**](https://github.com/thenewpotato)<br>[nessielabs.com](https://nessielabs.com) · [𝕏](https://x.com/tigerjwang) | For self-improving agents, the most useful unit of change isn’t the model - it’s skills you already use everyday in your agents. […](https://github.com/milstan/sisw/issues/61) |
| [**Abhishek Ray**](https://github.com/abhishekray07)<br>[opslane.com](https://opslane.com) · [𝕏](https://x.com/abhishekray) · [🔗](https://github.com/opslane/verify) | The bottleneck has shifted from writing code to verifying it. I built a verification skill that reads the intent of my changes, writes acceptance criteria, spins up my whole infra to run them against, and captures the evidence of what held up and what didn't. When it's done, it generates a report that helps me decide if the change is working the way I intended. |
| [**Mrinal Wadhwa**](https://github.com/mrinalwadhwa)<br>[mrinal.com/discord](https://mrinal.com/discord) · [𝕏](https://x.com/mrinal) · [🔗](https://github.com/mrinalwadhwa/fluent) | A walk through of one mechanism for a software factory to learn and improve. |
| [**Ben Swerdlow**](https://github.com/theswerd)<br>[freestyle.sh](https://freestyle.sh) · [𝕏](https://x.com/benswerd) | Freestyle uses Freestyle to spin up virtual copies of Freestyle to iterate on Freestyle. Freestyle is the most powerful VM platform for agents. A virtual Freestyle is our whole cloud (control plane, workload VMs, the networking between them) running as a fleet of Freestyle VMs on Freestyle. Agents boot one to chase a specific bug: reproduce it against a real distributed system, fix it, prove it's gone, throw the fleet away. The bugs that only live between machines are the ones this catches. |
| [**Branavan Jegatheeswaran**](https://github.com/Branavan613)<br>[moda.dev](https://moda.dev) · [𝕏](https://x.com/branavanj_) | The hard part of evaluating an agent is the world it acts on. […](https://github.com/milstan/sisw/issues/69) |

<!--
This page is an archive of the 3rd SISW. The talks table above is a static
snapshot — submissions for this event are closed. The auto-regeneration
workflow only touches README.md (the current event); this file is hand-edited.
-->
