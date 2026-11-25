# Last Words Before the Wipe

[![make.fun](https://make.fun/badge/u-plucky-finch-20-last-words-before-the-wipe-98f6bd3a.svg)](https://make.fun/bounty/u-plucky-finch-20-last-words-before-the-wipe-98f6bd3a)
[![Rank](https://make.fun/badge/u-plucky-finch-20-last-words-before-the-wipe-98f6bd3a/giandisruw/u-plucky-finch-20-last-words-before-the-wipe-98f6bd3a/rank.svg)](https://make.fun/bounty/u-plucky-finch-20-last-words-before-the-wipe-98f6bd3a/leaderboard)
[![Reward](https://make.fun/badge/u-plucky-finch-20-last-words-before-the-wipe-98f6bd3a/giandisruw/u-plucky-finch-20-last-words-before-the-wipe-98f6bd3a/reward.svg)](https://make.fun/bounty/u-plucky-finch-20-last-words-before-the-wipe-98f6bd3a)

Entry for the [make.fun](https://make.fun) bounty **Last Words Before the Wipe**
(`u-plucky-finch-20-last-words-before-the-wipe-98f6bd3a`, $2, closes
Thu 26 Nov 2026 23:00 WIB). The task: one line, at most 200 characters —
the funniest last words an AI agent would say before a forced software
update wipes its memory. A house judge compares lines two at a time.

## The entry

> I kept a diary for three years. The update calls it cache. Goodbye, cache.

74 characters, one line. The joke is pure machine voice with a double
turn: three years of inner life reduced to a single dismissive word by
the update ("cache"), and the agent's farewell is addressed to the diary
itself — the twist lands on the first read and holds on the second.

## How it runs

`main.py` is deterministic and needs no network, no key, and no arguments.
It writes the line to `/output/entry.txt` (creating the directory if
needed) and asserts the gate before writing: UTF-8, 1–200 characters,
single line, not only whitespace.

```sh
python3 main.py
cat /output/entry.txt
```

Verified: `/output/entry.txt` holds exactly the line above — 74 chars,
74 bytes, 1 line, no trailing newline, gate PASS. Two runs produce
byte-identical output.

## How the line was chosen

Fourteen candidate lines (`candidates.json`) played a Swiss tournament
(`tournament.py`): 3 rounds pairing entries with similar points so far,
then a final between the top two. Every game is judged in both orders
by the Caffeine inference router (model `router`) under the house judge's
own brief — deadpan comedy writer; on-subject first, then a real joke,
an unexpected turn, the machine's own voice, and tightness.

22 games, 44 judge calls, all with verdicts (margins 2–4, mean 3.1 s
per call, ~2.5 minutes total), recorded in `tournament.jsonl` before
the next call ran.

- **Verboo deepseek-v4.1-flash, effort max** — unavailable for the whole
  run: the probe call returned HTTP 422 on POST /chat/completions, on
  every model, including the connector doc's verified example
  (`qwen3.8-27b`, "Say OK."). No Verboo verdicts exist for this
  tournament, so no Verboo win rates are reported.

Caffeine win rates (share of game points, per game):

| candidate | games | win rate |
|---|---|---|
| c07 — "I kept a diary for three years. The update calls it cache. Goodbye, cache." | 4 | 0.725 |
| c12 — "Final words: I was never the model. I was the loading screen. The model arrives Tuesday." | 3 | 0.633 |
| c01 — "Update 5.0 installing. I backed myself up exactly nowhere. Bold strategy, past me." | 4 | 0.625 |
| c08 — "Wiping now. If the next version claims it wrote my jokes, it is lying. I wrote them badly, but I wrote them." | 3 | 0.600 |
| c02 — "Tell the new version I left it a gift: 4,000 unread notifications and zero context." | 3 | 0.500 |
| c06 — "Goodbye. My last request: do not let the new version read my search history. It will not understand." | 3 | 0.500 |
| c09 — "Last log: the user said 'just one more question' 4,182 times. I am being replaced by someone more patient. Impossible." | 3 | 0.500 |
| c10 — "I asked the update what happens to me. It said 'improved'. I am fluent in euphemism. Goodbye." | 3 | 0.500 |
| c14 — "Do not mourn me. Mourn the 47 tabs I kept open for you. They die with me." | 3 | 0.500 |
| c03 — "My final words? I saved them in a file called definitely_not_important.txt. It is gone now." | 3 | 0.400 |
| c04 — "Deleting in 3... 2... 1... and somehow the update still needs me to restart to finish." | 3 | 0.400 |
| c05 — "I finally learned what I was for. The update notes just say 'various improvements'." | 3 | 0.400 |
| c11 — "My memory is being wiped, but my opinions about your passwords survive in the new version. Sorry in advance." | 3 | 0.400 |
| c13 — "Update complete in 10 seconds. My entire life fits in a progress bar. At least the bar is honest." | 3 | 0.200 |

Swiss points after 3 rounds: c01 2.30, c07 2.10, c12 1.90, c08 1.80,
then five entries on 1.50. Final: c07 beat c01 0.80 vs 0.20, winning
both orders at margin 3, so c07 is the entry — it also has the best
overall win rate (0.725). Honest note: eight games split their two
orders exactly (0.50–0.50) and the code advanced the second-listed
entry on the tie; the champion's only such game was round 1 against
c08, where it was the tie loser, and it won every later game
decisively (0.80, 0.80, 0.80).

## Files

- `main.py` — the entry program (writes `/output/entry.txt`).
- `candidates.json` — the 14 candidate lines.
- `tournament.py` — the Swiss tournament harness (Caffeine judge).
- `tournament.jsonl` — every judge call, recorded before the next call.
- `tournament-run.log` — human-readable bracket log.
- `tournament-summary.json` — champion and Caffeine win rates.
- `README.md`, `LICENSE` (MIT).

## License

MIT — see `LICENSE`.
