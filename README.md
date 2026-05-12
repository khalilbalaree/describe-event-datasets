# DescribeEvent Datasets

Seven event-prediction datasets following the temporal point process (TPP) formulation. Each dataset is a JSONL file with one sequence per line; each line describes a marked temporal point process, where every event comes with a natural-language description.

## Dataset format

Every dataset shares these fields:

| Field | Type | Meaning |
|---|---|---|
| `seq_idx` | int | Sequence index within the split |
| `seq_len` | int | Number of events in this sequence |
| `description` | str | Natural-language summary of the sequence (entity, time window, source) |
| `metadata` | str (JSON-encoded dict) | Structured context (IDs, entities, time range, type dictionary, …) |
| `type_event` | list[str], length `seq_len` | Discrete event-type label for each event |
| `type_text` | list[str], length `seq_len` | One-sentence natural-language rendering of each event |
| `time_since_start` | list[float], length `seq_len` | Time elapsed since the first event (units vary; see `metadata.time_unit` when present) |
| `time_since_last_event` | list[float], length `seq_len` | Inter-arrival time from the previous event |

## Dataset Statistics

| Dataset | Rows | Events | Event types | Seq len (min/med/max) | File size |
|---|---:|---:|---:|---|---:|
| amazon_review_events | 229 | 13,299 | 40 | 50 / 56 / 78 | 4.1 MB |
| earthquake_region_events | 215 | 10,510 | 8 | 31 / 50 / 50 | 3.7 MB |
| gdelt_news_events | 179 | 13,779 | 7 | 40 / 82 / 100 | 1.5 MB |
| github_repo_events | 373 | 25,576 | 8 | 60 / 68 / 80 | 12 MB |
| github_user_events | 382 | 33,856 | 8 | 80 / 88 / 100 | 17 MB |
| nba_quarter_events | 286 | 29,102 | 9 | 90 / 103 / 110 | 5.5 MB |
| wikipedia_edit_events | 276 | 22,063 | 6 | 63 / 80 / 80 | 4.4 MB |

### Domain summaries

- **amazon_review_events** — A user's Amazon product-review timeline within a
  parent category (e.g., Electronics); event type is the product
  sub-category, text is the rating + review snippet.
- **earthquake_region_events** — Global seismic activity bucketed into a
  fiscal quarter; event type is the tectonic zone, text describes
  magnitude / location / station count.
- **gdelt_news_events** — Geopolitical interactions between a country pair
  from the GDELT database; event type is the CAMEO category (public
  statement, armed conflict, …), text is a one-line news summary.
- **github_repo_events** — One week of activity on a public GitHub
  repository; event type ∈ {push, pr_opened, comment, …}, text describes
  the action and actor.
- **github_user_events** — One week of cross-repo activity for a single
  GitHub user; same event-type vocabulary as the repo dataset.
- **nba_quarter_events** — Play-by-play events from one quarter of an NBA
  game; event type ∈ {made_fg, missed_fg, rebound, foul, …}, text is the
  commentary line.
- **wikipedia_edit_events** — Edit history for a Wikipedia article; event
  type ∈ {content_addition, content_removal, revert, …}, text describes
  editor + byte delta + summary.
