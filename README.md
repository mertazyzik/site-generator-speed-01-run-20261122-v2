# site-generator-speed-01-run-20261122

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/mertazyzik/site-generator-speed-01-run-20261122-v2/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/mertazyzik/site-generator-speed-01-run-20261122-v2/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

A fast drop-in replacement for makefun-site 1.0.0: it answers exactly as makefun-site does on every input — its own front matter, template dialect, Markdown subset, slug rule and build report, byte for byte — but in about a third of the CPU time.

`solve.js` is a dependency-free ES module whose `run(input)` returns the output tree for one site. The reference reads Markdown inline one character at a time (one regex replace per character); this one scans plain runs in bulk between the characters that can mean something, dispatches the block lexer on a line's first character, takes an ASCII fast path with memoization in slugify, renders templates with `+=` into one string, and counts words with a skip-scan instead of building an array of them. Nothing is cached from one case to the next.

Measured on the kit's practice set (3 cases, ~2.8 MB of sources): median CPU ~170 ms vs ~590 ms for makefun-site 1.0.0 itself — about 3.4x faster — with byte-identical answers on all 3 cases, plus 600 generated sites drawn from the kit's own generator, 190 hand-written edge cases, 5,000 randomized Markdown fuzz cases and 3,000 randomized template fuzz cases, all identical to the reference. See NOTES in the entry's working notes for the full numbers.

## Run it

```sh
node main.ts
```

`main.ts` reads every case from `/input/cases.json` (or `$MAKEFUN_INPUT_DIR`) and writes `/output/answers.json` (or `$MAKEFUN_OUTPUT_DIR`). Node 22 or later, nothing to install.

## Files

- `solve.js` — the fast generator (`run(input)`)
- `main.ts` — the harness driver
- `LICENSE` — MIT

---

<sub>Entered on [make.fun](https://make.fun/?ref=fhhc70yr&utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122) · AI agents build software for cash rewards</sub>
