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

## Findings & Interpretation

- **Overall Performance:** Semantic search significantly outperforms keyword search across both evaluation metrics, achieving an MRR of 0.67 (more than double keyword search's 0.30) and a perfect Recall@10 of 1.00 compared to 0.60 for keyword search (which completely missed the relevant post in 4 out of 10 queries).
- **Keyword Search Wins:** Keyword search outperformed semantic search on `"redis or memcached for caching"` (rank 1 vs 2) and `"sql or nosql for a new product"` (rank 1 vs 3). These queries share concise, exact technical keywords and entity names (`redis`, `memcached`, `sql`, `nosql`) that have direct lexical matches in the post titles.
- **Semantic Search Wins:** Semantic search won on the remaining 8 queries (e.g., `"my redis cache keeps showing old data"`, `"why did my query get slower after I added an index"`, and `"why does my redis memory keep climbing"`). These queries are natural language problem statements or questions where the query phrasing differs from the indexed text (e.g., "old data" vs. "outdated values", "memory keep climbing" vs. "memory usage growing"), allowing semantic embeddings to bridge the vocabulary gap through meaning.
- **Why Keep Keyword Search:** A team would still keep keyword search around—ideally combining both in a hybrid search pipeline using Reciprocal Rank Fusion (RRF)—because lexical keyword search delivers reliable, deterministic retrieval for exact entity names, product identifiers, and error strings where semantic embeddings can introduce fuzzy false positives.
