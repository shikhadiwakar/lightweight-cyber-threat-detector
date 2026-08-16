# Feature Documentation Table

Fill this in **after** you've loaded your actual CICIDS2017 file and run
`df.columns`, `df.info()`, and `df.head()` on it in `01_dataset_exploration.ipynb`.

**Do not guess column names ahead of time — different CICIDS2017 file versions have
slightly different column names/spacing (e.g. a leading space before `Label` is common).
Copy the real column names from your actual `df.columns` output.**

## How to fill this in

For every column in your dataset, add one row:

- **Feature** — the exact column name from `df.columns`.
- **Meaning** — what it represents, in plain language (use `attack_categories.md` and
  `references.md` — the CICIDS2017 paper describes how CICFlowMeter computes each flow
  feature — to help explain the less obvious ones).
- **Data Type** — what `df.dtypes` / `df.info()` says (`int64`, `float64`, `object`,
  etc.), and whether that's actually correct (e.g. a column of numbers stored as text
  should be flagged).
- **Keep / Remove** — your decision for the feature-engineering stage.
- **Reason** — why. Common reasons to **remove**: it's a pure identifier (e.g. Flow ID,
  raw Source/Destination IP, raw timestamp) that could cause data leakage or overfitting
  rather than teach the model real behavioural patterns; it's constant/near-constant
  across all rows; it duplicates another feature. Common reasons to **keep**: it
  describes traffic volume, timing, packet, protocol, or port *behaviour* that could
  genuinely help distinguish attacks from normal traffic.

## Table

| Feature | Meaning | Data Type | Keep/Remove | Reason |
|---|---|---|---|---|
| _(example)_ Flow Duration | Total duration of the flow in microseconds | float64 | Keep | Behavioural — attacks often have distinctly short/long flow durations |
| _(example)_ Source IP | The IP address that started the flow | object | Remove | Identifier — the model could "memorize" specific IPs seen in training instead of learning general attack behaviour, which would not generalize to a real deployment (data leakage risk) |
| | | | | |
| | | | | |
| | | | | |

Add as many rows as you have columns. This table becomes Stage 4's main deliverable
alongside the feature-engineering notebook — it's the evidence that every column was a
deliberate decision, not guesswork.

## A note on data leakage (read before filling in "Keep/Remove")

Some columns look harmless but leak information a real detector wouldn't have, or let
the model "cheat" by memorizing identities instead of learning patterns:

- **Flow ID** — often just a concatenation of IP:port:IP:port:protocol. Keeping it risks
  the model learning specific flow identities instead of general behaviour.
- **Source IP / Destination IP** — same risk; also, a model trained to recognize "attacks
  come from IP X" will fail completely against an attacker using a different IP.
- **Timestamp** — if attacks in your captured file happen to cluster in a specific time
  window, the model could learn "traffic at 14:32 = attack" instead of learning real
  traffic *behaviour*. That would not generalize.
- **Source Port / Destination Port** — these are more nuanced. A destination port (e.g.
  22 for SSH, 80 for HTTP) can be genuinely informative (some attacks target specific
  services), so this is a "keep, but think about it" case rather than an automatic
  removal — explain your reasoning either way.

When in doubt, ask: *"Would this column still be available and meaningful for a brand
new, real-time network flow the model has never seen before?"* If not, it's a leakage
risk.
