# Retrieval-Augmented-Generation (RAG):

- Retrieval-Augmented Generation (RAG) pipeline, chunking is the critical preprocessing step of breaking down large, unstructured documents into smaller, semantically meaningful segments.

# Purpose of Chunking:

- The primary purpose of chunking in RAG is to transform raw data into "AI-ready" pieces that can be efficiently indexed, retrieved, and processed by both embedding models and Large Language Models (LLMs). Because both these models have strict context window limits (a maximum number of tokens they can handle at once), they cannot ingest entire books or lengthy reports in a single pass

# Why Chunking is Essential for RAG

- Context Window Management: Ensures retrieved content fits within the LLM's prompt limit without truncating vital information.
- Retrieval Accuracy: Smaller, focused chunks allow for more precise vector embeddings. Large chunks can "dilute" specific topics, making it harder for a vector database to find the exact answer to a niche query.
- Reduced Hallucinations: By providing the LLM with only highly relevant snippets rather than overwhelming it with noise from an entire document, the model is less likely to lose focus and fabricate incorrect information.
- Cost & Performance: Processing smaller, targeted segments reduces computational overhead, speeds up response times, and lowers token-based API costs.

# Common Chunking Strategies & Examples

| S.No | Strategy       | How it Works                                                                                                      | Best For                                                             | Example                                                                                    |
| ---- | -------------- | ----------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| 1    | Fixed-Size     | Splits text into a set number of characters or tokens, often with a small "overlap" to maintain continuity.       | Simple documents, FAQs, or quick prototyping.                        | A 500-token chunk with a 50-token overlap to ensure sentences aren't lost at the cut.      |
| 2    | Recursive      | Uses a hierarchy of separators (e.g., paragraphs first, then sentences, then words) until the target size is met. | Articles, blog posts, and research papers.                           | Breaking a long report by its double-newline \\n\\n paragraph marks first.                 |
| 3    | Document-Based | Respects the document's native structure like headers, tables, or code syntax.                                    | Markdown files, HTML pages, or Python/Java code.                     | Splitting a README at every \## Header to keep sections together.                          |
| 4    | Semantic       | Uses embeddings to identify "meaning shifts" and splits only when the topic actually changes.                     | Complex, dense, or unstructured legal/medical texts.                 | Grouping sentences together as long as their similarity score stays above a set threshold. |
| 5    | Agentic        | Uses a smaller LLM "agent" to act like a human editor, deciding where to cut based on logical flow.               | High-value, complex documents where quality is worth the extra cost. | An agent reading a dense contract and marking boundaries where clauses begin and end.      |