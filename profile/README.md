# 🌊 marola

A friendly guide to the sea near you: which beach is good for swimming today, and the best hour
tomorrow. It is built from public data, in the open, as citizen science, and it says "no data"
when it does not know.

**[marola.dev](https://marola.dev/)**: the live map (Florianópolis, Rio de Janeiro, Salvador) ·
**[docs.marola.dev](https://docs.marola.dev/)**: using and building marola

## Why

- **Open and non-profit.** Much of Brazil's ocean data sits with private holders, and nobody can
  forecast water quality, climate disasters or environmental accidents without it. A non-profit
  that promises to share everything can ask for that data; one more company could not.
- **Water quality first.** Sanitation in Brazil is far from solved, so marola starts with the
  question "can I go in this water?". A national bathing-water ranking is
  [under discussion](https://github.com/marola-dev/marola/discussions/676).
- **A water super app.** One place that hands you the answer, not the tools: what Sequoia calls
  [services as software](https://sequoiacap.com/article/services-the-new-software).
- **Open source, for the long term.** With AI, code is no longer the secret. Brazil needs
  projects that outlive the people and the governments that started them.
- **Partners, not money.** We welcome storage, GPU time or data from companies, credited
  discreetly on the site. No ads, no tracking.

## How it is built

One project, many small repos: a distributed monolith. A shared plan and rules let AI agents see
the whole picture, while each repo keeps its own tests and releases and pins the others'
published versions instead of reading their code.

### Why an umbrella

marola started as one repo. By September 2026 that one tree forced one build on everything: a
CSS change to the map waited on a Scala compile, and parallel agent sessions needed 30+ worktrees
to stay out of each other's way. Splitting into separate repos fixes the builds but loses what
the single repo did best: an agent could see the whole project at once.

The umbrella keeps both. [marola](https://github.com/marola-dev/marola) holds no code, only the
team layer (plans, rules, the phase list, the docs site) and every other repo as a git submodule.
Clone it with `--recurse-submodules` and the whole project is one directory again, with the
shared rules at the root and each repo's own rules inside it. Each repo still builds, tests and
releases alone, and talks to the others only through versioned artifacts it pins.

The idea is an old one: a "meta-repo" that pins many repos into one workspace, as Android's
[`repo`](https://source.android.com/docs/setup/reference/repo) manifest does. marola adopted it
in [MIP-0070](https://docs.marola.dev/6-MIPs/MIP-0070-umbrella-and-polyrepo-split/) (2026-09-30),
which also lists the alternatives it turned down.

<p align="center"><img src="https://raw.githubusercontent.com/marola-dev/marola/main/docs/img/umbrella.svg" alt="How marola's repositories depend on each other" width="760" /></p>

| Repo | What it holds |
|---|---|
| [marola](https://github.com/marola-dev/marola) | The umbrella: plans (MIPs), rules, the docs site, every repo as a submodule |
| [marola-app](https://github.com/marola-dev/marola-app) | The product: Scala 3 + Kyo, the score and safety veto, the CLI and MCP server |
| [marola-site](https://github.com/marola-dev/marola-site) | The map at marola.dev |
| [marola-oods](https://github.com/marola-dev/marola-oods) | The Open Ocean Data Store: an open archive of beaches and water quality |
| [marola-corpus](https://github.com/marola-dev/marola-corpus) | The sourced ocean knowledge marola answers from |
| [marola-ml](https://github.com/marola-dev/marola-ml) | Prompt compilation, the marola-sea fine-tune, the benchmark gate |
| [marola-devkit](https://github.com/marola-dev/marola-devkit) | Shared dev tooling, hooks, workflows and the Claude Code plugin |
| [marola-skills](https://github.com/marola-dev/marola-skills) | The catalogue of every Claude Code skill and subagent across the repos |
| [marola-agents](https://github.com/marola-dev/marola-agents) | The inventory of every agent marola uses or plans |
| [marola-research](https://github.com/marola-dev/marola-research) | Science |

**Help out:** use the map and tell us when it is wrong, or open an
[issue](https://github.com/marola-dev/marola/issues) in Portuguese or English. More in
[Contributing](https://docs.marola.dev/3-Ways-of-working/CONTRIBUTING/).
