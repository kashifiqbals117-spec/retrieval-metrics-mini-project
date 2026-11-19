# Retrieval Metrics Evaluation Results

## Evaluation Table

| Query | Keyword rank | Semantic rank |
|---|---|---|
| my redis cache keeps showing old data | 8 | 1 |
| how do I add semantic search to a table I already have | miss | 2 |
| redis or memcached for caching | 1 | 2 |
| why did my query get slower after I added an index | miss | 1 |
| what does ACID actually guarantee | 2 | 1 |
| how do I keep my postgres online while changing the schema | 6 | 3 |
| my background jobs stop after every deploy | miss | 2 |
| how do I let my database accept more writes per second | 4 | 1 |
| sql or nosql for a new product | 1 | 3 |
| why does my redis memory keep climbing | miss | 2 |
| **Summary** | **MRR 0.30 · Recall@10 0.60** | **MRR 0.67 · Recall@10 1.00** |

## Interpretation

Overall, semantic search performs substantially better than keyword search on both metrics, scoring a Mean Reciprocal Rank (MRR) of 0.67 compared to 0.30 and achieving a perfect Recall@10 of 1.00 compared to 0.60, where keyword search missed the correct document entirely for 4 out of 10 queries. Keyword search specifically won on two queries—`redis or memcached for caching` (rank 1 vs 2) and `sql or nosql for a new product` (rank 1 vs 3)—which both feature concise, exact domain entities and technical keywords that appear verbatim in the document titles. In contrast, semantic search won on the remaining eight queries (such as `my redis cache keeps showing old data`, `why did my query get slower after I added an index`, and `why does my redis memory keep climbing`), which are phrased as natural language questions and symptom descriptions whose vocabulary diverges from the document text. A team would still keep the weaker keyword system around in a hybrid search pipeline (using Reciprocal Rank Fusion) because keyword search guarantees deterministic, high-precision retrieval for rare technical terms, acronyms, and exact product names where semantic embeddings can be noisy or imprecise.
