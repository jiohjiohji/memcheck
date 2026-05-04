# Health Scoring

## When to use
When working on files in `src/core/`.

## Staleness (Ebbinghaus Decay Model)
- Formula: R(t) = e^(-t/S)
- R = retention strength (0.0 to 1.0). Higher = healthier.
- t = days since last access
- S = stability (starts 1.0, multiply by 1.5 on each recall)
- Prune threshold: R(t) < 0.15

## Redundancy
- Cosine similarity > 0.92 between two entries = near-duplicate
- If embeddings unavailable, use Jaccard similarity on tokenized content (threshold 0.85)
- Keep the most-recently-accessed entry from each duplicate cluster

## Bloat Rate
- bloat_ratio = entries_added_last_30d / entries_retrieved_last_30d
- Healthy: < 2.0 | Warning: 2.0–4.0 | Critical: > 4.0

## Composite Score
- Weights: staleness 40%, redundancy 30%, bloat 30%
- Grade: A (80+), B (60–79), C (40–59), D (20–39), F (<20)

## Testing
- Every scorer needs tests for: empty input, single entry, all-bad, all-good, mixed
- Performance: scoring 10K entries must complete in under 2 seconds