# Retrieval Evaluation Results and Interpretation

## Results Table

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

## Findings and Interpretation

Overall, semantic search outperforms keyword search by a wide margin across both metrics, achieving an MRR of 0.67 compared to 0.30, and a perfect Recall@10 of 1.00 compared to 0.60. Keyword search only won on queries containing exact terminology and proper nouns, specifically `redis or memcached for caching` and `sql or nosql for a new product`, where users searched for direct product comparisons whose exact tokens closely matched the document titles. In contrast, semantic search dominated conversational, symptom-focused queries like `why does my redis memory keep climbing` and `my background jobs stop after every deploy`, successfully capturing conceptual intent and synonyms (such as "climbing" vs. "growing" or "jobs stop" vs. "worker queue dies") where keyword search missed completely. A team would still keep the weaker keyword search system around—typically combining both via hybrid search (such as Reciprocal Rank Fusion)—because keyword matching delivers deterministic precision for exact keywords, error codes, and technical identifiers that embedding models can blur or dilute.
