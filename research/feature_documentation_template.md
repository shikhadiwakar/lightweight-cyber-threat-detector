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
| `' Destination Port'` | Port number on the receiving end of the flow (e.g. 80 = HTTP, 22 = SSH) | int64 (categorical identifier, not a quantity) | | |
| `' Flow Duration'` | Total time the flow lasted (microseconds) | int64 | | |
| `' Total Fwd Packets'` | Number of packets sent forward (client → server) | int64 | | |
| `' Total Backward Packets'` | Number of packets sent backward (server → client) | int64 | | |
| `'Total Length of Fwd Packets'` | Total bytes of payload sent forward | int64 | | |
| `' Total Length of Bwd Packets'` | Total bytes of payload sent backward | int64 | | |
| `' Fwd Packet Length Max'` | Size of the largest forward packet | int64 | | |
| `' Fwd Packet Length Min'` | Size of the smallest forward packet | int64 | | |
| `' Fwd Packet Length Mean'` | Average forward packet size | float64 | | |
| `' Fwd Packet Length Std'` | Standard deviation of forward packet sizes | float64 | | |
| `'Bwd Packet Length Max'` | Size of the largest backward packet | int64 | | |
| `' Bwd Packet Length Min'` | Size of the smallest backward packet | int64 | | |
| `' Bwd Packet Length Mean'` | Average backward packet size | float64 | | |
| `' Bwd Packet Length Std'` | Standard deviation of backward packet sizes | float64 | | |
| `'Flow Bytes/s'` | Data transfer rate of the flow (bytes per second) | float64 (contains `inf`/`NaN` from zero-duration flows) | | |
| `' Flow Packets/s'` | Packet rate of the flow (packets per second) | float64 (contains `inf`/`NaN` from zero-duration flows) | | |
| `' Flow IAT Mean'` | Average time gap between consecutive packets in the flow (IAT = inter-arrival time, microseconds) | float64 | | |
| `' Flow IAT Std'` | Standard deviation of those gaps (how irregular the timing is) | float64 | | |
| `' Flow IAT Max'` | Longest gap between two packets in the flow | int64 | | |
| `' Flow IAT Min'` | Shortest gap between two packets in the flow | int64 | | |
| `'Fwd IAT Total'` | Total of all time gaps between forward packets | int64 | | |
| `' Fwd IAT Mean'` | Average gap between forward packets | float64 | | |
| `' Fwd IAT Std'` | Standard deviation of forward gaps | float64 | | |
| `' Fwd IAT Max'` | Longest gap between forward packets | int64 | | |
| `' Fwd IAT Min'` | Shortest gap between forward packets | int64 | | |
| `'Bwd IAT Total'` | Total of all time gaps between backward packets | int64 | | |
| `' Bwd IAT Mean'` | Average gap between backward packets | float64 | | |
| `' Bwd IAT Std'` | Standard deviation of backward gaps | float64 | | |
| `' Bwd IAT Max'` | Longest gap between backward packets | int64 | | |
| `' Bwd IAT Min'` | Shortest gap between backward packets | int64 | | |
| `'Fwd PSH Flags'` | Number of times the TCP PSH ("push data now") flag was set in forward packets | int64 | | |
| `' Bwd PSH Flags'` | Number of times the PSH flag was set in backward packets | int64 | | |
| `' Fwd URG Flags'` | Number of times the TCP URG ("urgent data") flag was set in forward packets | int64 | | |
| `' Bwd URG Flags'` | Number of times the URG flag was set in backward packets | int64 | | |
| `' Fwd Header Length'` | Total bytes of protocol headers in forward packets | int64 | | |
| `' Bwd Header Length'` | Total bytes of protocol headers in backward packets | int64 | | |
| `'Fwd Packets/s'` | Forward packets per second | float64 | | |
| `' Bwd Packets/s'` | Backward packets per second | float64 | | |
| `' Min Packet Length'` | Smallest packet in the flow, either direction | int64 | | |
| `' Max Packet Length'` | Largest packet in the flow, either direction | int64 | | |
| `' Packet Length Mean'` | Average packet size across the whole flow | float64 | | |
| `' Packet Length Std'` | Standard deviation of packet sizes across the flow | float64 | | |
| `' Packet Length Variance'` | Variance of packet sizes (the square of the std) | float64 | | |
| `'FIN Flag Count'` | Number of packets with the TCP FIN (connection close) flag | float64 (integer-valued count) | | |
| `' SYN Flag Count'` | Number of packets with the TCP SYN (connection open) flag | float64 (integer-valued count) | | |
| `' RST Flag Count'` | Number of packets with the TCP RST (connection reset) flag | float64 (integer-valued count) | | |
| `' PSH Flag Count'` | Number of packets with the PSH flag | float64 (integer-valued count) | | |
| `' ACK Flag Count'` | Number of packets with the ACK (acknowledgement) flag | float64 (integer-valued count) | | |
| `' URG Flag Count'` | Number of packets with the URG flag | float64 (integer-valued count) | | |
| `' CWE Flag Count'` | Number of packets with the CWR (congestion window reduced) flag; the name is a known typo in the dataset | float64 (integer-valued count) | | |
| `' ECE Flag Count'` | Number of packets with the ECE (explicit congestion notification echo) flag | float64 (integer-valued count) | | |
| `' Down/Up Ratio'` | Ratio of download (backward) to upload (forward) traffic | float64 | | |
| `' Average Packet Size'` | Average size of a packet in the flow | float64 | | |
| `' Avg Fwd Segment Size'` | Average size of forward segments | float64 | | |
| `' Avg Bwd Segment Size'` | Average size of backward segments | float64 | | |
| `' Fwd Header Length.1'` | Duplicate copy of `Fwd Header Length` (pandas added `.1` because the name appeared twice in the CSV) | float64 (integer-valued; duplicate column) | | |
| `'Fwd Avg Bytes/Bulk'` | Average bytes per "bulk" transfer in the forward direction | float64 (integer-valued) | | |
| `' Fwd Avg Packets/Bulk'` | Average packets per bulk transfer, forward | float64 (integer-valued) | | |
| `' Fwd Avg Bulk Rate'` | Average bulk transfer rate, forward | float64 (integer-valued) | | |
| `' Bwd Avg Bytes/Bulk'` | Average bytes per bulk transfer, backward | float64 (integer-valued) | | |
| `' Bwd Avg Packets/Bulk'` | Average packets per bulk transfer, backward | float64 (integer-valued) | | |
| `'Bwd Avg Bulk Rate'` | Average bulk transfer rate, backward | float64 (integer-valued) | | |
| `'Subflow Fwd Packets'` | Average number of forward packets per subflow | float64 (integer-valued count) | | |
| `' Subflow Fwd Bytes'` | Average forward bytes per subflow | float64 (integer-valued) | | |
| `' Subflow Bwd Packets'` | Average number of backward packets per subflow | float64 (integer-valued count) | | |
| `' Subflow Bwd Bytes'` | Average backward bytes per subflow | float64 (integer-valued) | | |
| `'Init_Win_bytes_forward'` | TCP window size (receive buffer, bytes) advertised in the first forward packet; `-1` when there's no TCP handshake | float64 (integer-valued; `-1` is a placeholder, not a real size) | | |
| `' Init_Win_bytes_backward'` | Same, for the first backward packet | float64 (integer-valued; `-1` is a placeholder, not a real size) | | |
| `' act_data_pkt_fwd'` | Number of forward packets that carry at least 1 byte of actual data | float64 (integer-valued count) | | |
| `' min_seg_size_forward'` | Smallest TCP segment header size seen in the forward direction | float64 (integer-valued) | | |
| `'Active Mean'` | Average time the flow was active before going idle | float64 | | |
| `' Active Std'` | Standard deviation of active periods | float64 | | |
| `' Active Max'` | Longest active period | float64 (integer-valued) | | |
| `' Active Min'` | Shortest active period | float64 (integer-valued) | | |
| `'Idle Mean'` | Average time the flow was idle before becoming active again | float64 | | |
| `' Idle Std'` | Standard deviation of idle periods | float64 | | |
| `' Idle Max'` | Longest idle period | float64 (integer-valued) | | |
| `' Idle Min'` | Shortest idle period | float64 (integer-valued) | | |
| `' Label'` | The class of the flow: `BENIGN` or the attack type (e.g. DoS, PortScan) | object (string; must be encoded to numbers before training) | | |

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
