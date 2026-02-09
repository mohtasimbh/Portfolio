---
title: "Natural Language Search Engine for Enterprise Knowledge Base"
excerpt: "Developed a semantic search system enabling employees to find information across 4.7 million documents using natural language queries, improving search success rate from 34% to 89% and reducing average time-to-answer from 23 minutes to 47 seconds."
collection: portfolio
---

## Project Overview

Built an intelligent search platform for a 75,000-employee professional services firm, unifying search across SharePoint, Confluence, email archives, and proprietary databases. The system understands natural language queries, retrieves semantically relevant results, and generates AI-powered answer summaries.

## The Challenge

Knowledge discovery was the organization's biggest productivity drain:

- **Fragmented information:** Content spread across 14 different platforms
- **Search failure:** Existing keyword search returned useful results only 34% of the time
- **Time wasted:** Average employee spent 2.4 hours daily searching for information
- **Duplicate work:** 40% of deliverables duplicated existing work that couldn't be found
- **Expertise location:** No way to identify who knew what
- **Onboarding friction:** New employees took 6 months to become productive

Requirements:

- Unified search across all knowledge repositories
- Natural language query understanding
- Semantic matching beyond keyword matching
- AI-generated answer summaries
- Expertise identification
- Personalized results based on role and history
- Enterprise security and access control compliance

## Technical Architecture

### Data Ingestion Layer

**Connectors built:**

- SharePoint Online (documents, lists, pages)
- Confluence Cloud (pages, attachments, comments)
- Microsoft Exchange (email archives, shared mailboxes)
- Salesforce (accounts, opportunities, cases)
- Custom SQL databases (client matter system, time tracking)
- File shares (legacy document repositories)
- Slack (channel history, files)

**Ingestion pipeline:**

- Change detection for incremental updates
- Content extraction (text, metadata, structure)
- Document parsing (PDF, Office, HTML, images with OCR)
- Chunking strategy for long documents
- Rate limiting and backpressure handling
- Dead letter queue for failed documents

**Scale:**

- 4.7 million documents indexed
- 23 billion tokens of text
- Daily delta processing: ~47,000 documents
- Full re-index capability within 48 hours

### Embedding and Indexing

**Embedding model:**

- Fine-tuned e5-large-v2 on domain-specific corpus
- Training data: 500,000 query-document pairs from search logs
- Hard negative mining from failed searches
- Contrastive learning with in-batch negatives
- Evaluation on held-out relevance judgments

**Chunking strategy:**

- Recursive splitting respecting document structure
- Overlap between chunks for context preservation
- Section-aware splitting (headers, paragraphs, lists)
- Metadata preservation (source, date, author, permissions)
- Average chunk size: 512 tokens

**Vector database:**

- Pinecone for vector storage and retrieval
- Namespaces for multi-tenant isolation
- Metadata filtering for access control
- Hybrid search combining dense and sparse

**Sparse index:**

- BM25 index for keyword matching
- Custom tokenization for domain terms
- Acronym and abbreviation expansion
- Entity recognition and indexing

### Query Processing

**Query understanding:**

- Intent classification (informational, navigational, transactional)
- Entity extraction (project names, client names, people, dates)
- Query expansion with synonyms and related terms
- Acronym resolution from organization glossary
- Spelling correction with domain vocabulary

**Query transformation:**

```
User query: "What's our cloud migration approach for financial clients?"

Expanded query:
- Original: cloud migration approach financial clients
- Entities: [industry:financial_services]
- Expanded: cloud migration strategy methodology banking insurance finserv
- Intent: informational_methodology
```

**Retrieval strategy:**

- Hybrid search: dense (0.7) + sparse (0.3) weighted combination
- Initial retrieval: 100 candidates
- Cross-encoder reranking: top 100 → top 20
- Diversity injection to avoid redundant results
- Personalization boost based on user history

### Answer Generation

**RAG pipeline:**

1. Retrieve relevant chunks (top 10)
2. Assess chunk relevance and extract key passages
3. Generate answer with citations
4. Fact-check answer against sources
5. Format with source links

**LLM integration:**

- Claude for answer generation (accuracy priority)
- Streaming response for perceived latency
- Context window management for long retrievals
- Prompt engineering for citation accuracy

**Answer format:**

```
Based on our methodology documentation, our cloud migration approach
for financial services clients follows a five-phase model:

1. **Assessment**: Evaluate current infrastructure and regulatory requirements [1]
2. **Planning**: Develop migration roadmap with compliance checkpoints [1][2]
3. **Pilot**: Migrate non-critical workloads to validate approach [2]
4. **Migration**: Execute phased migration with rollback capability [3]
5. **Optimization**: Continuous improvement and cost optimization [3]

Key considerations for financial clients include SOC 2 compliance,
data residency requirements, and regulatory reporting capabilities [2].

Sources:
[1] Cloud Migration Methodology v3.2 - SharePoint
[2] Financial Services Industry Playbook - Confluence
[3] AWS Migration Guide - Internal Wiki
```

### Personalization

**User context:**

- Role and department
- Project history
- Search and click history
- Expertise areas (inferred)
- Collaboration network

**Personalization signals:**

- Recent projects boost related content
- Department-specific terminology matching
- Previously accessed documents boosted
- Colleague-accessed content boosted
- Expertise-based result diversification

**Cold start handling:**

- Role-based defaults for new employees
- Onboarding content prioritization
- Gradual personalization as signals accumulate

### Expertise Finding

**People search:**
"Who knows about AWS Lambda?" returns:

- Authors of Lambda-related documents
- People who've worked on Lambda projects
- People frequently asking/answering Lambda questions
- Weighted by recency and depth of expertise

**Expertise inference:**

- Document authorship analysis
- Project participation
- Communication patterns (anonymized)
- Self-declared skills (LinkedIn, internal profiles)
- Endorsements and collaboration patterns

### Security and Compliance

**Access control:**

- Permission sync from source systems
- Row-level security in vector database
- Query-time filtering based on user permissions
- No content shown user shouldn't access

**Audit logging:**

- All queries logged with user context
- Retrieved documents tracked
- Generated answers stored
- Compliance reporting capability

**Data handling:**

- No PII in embeddings
- Sensitive document classification
- Retention policies enforced
- GDPR right-to-deletion supported

## Results

### Search Performance

| Metric                   | Before     | After      |
| ------------------------ | ---------- | ---------- |
| Search success rate      | 34%        | 89%        |
| Time to find answer      | 23 minutes | 47 seconds |
| Queries per employee/day | 3.2        | 8.7        |
| Click-through rate       | 18%        | 67%        |
| Zero-result queries      | 23%        | 2%         |

### Business Impact

**Productivity:**

- Time saved per employee: 1.8 hours/day
- Organization-wide: 3.4 million hours annually
- Monetary value: $127M annually (at average billing rate)

**Quality:**

- Duplicate work reduced 62%
- Proposal reuse increased 340%
- Knowledge transfer to new hires accelerated (6 months → 8 weeks)

**Engagement:**

- Daily active users: 67,000 (89% of workforce)
- Queries per day: 583,000
- User satisfaction: 91%

### Technical Metrics

| Metric                 | Value                   |
| ---------------------- | ----------------------- |
| Query latency (P50)    | 1.2 seconds             |
| Query latency (P99)    | 3.8 seconds             |
| Answer generation time | 2.1 seconds average     |
| Index freshness        | <15 minutes for changes |
| System availability    | 99.95%                  |

## Technologies Used

- **Embeddings:** Custom fine-tuned e5-large-v2, sentence-transformers
- **Vector DB:** Pinecone
- **Sparse Search:** Elasticsearch
- **LLM:** Claude (Anthropic), with fallback to GPT-4
- **Orchestration:** LangChain, custom retrieval pipeline
- **Backend:** Python, FastAPI, Celery
- **Frontend:** React, TypeScript
- **Infrastructure:** AWS (EKS, Lambda, S3), Terraform

## Lessons Learned

**Retrieval quality > generation quality:**

- If you retrieve wrong documents, the best LLM can't save you
- Invested 70% of effort in retrieval, 30% in generation
- Evaluation datasets essential for retrieval tuning
- Hybrid search consistently outperformed pure semantic

**Domain adaptation matters:**

- Off-the-shelf embeddings underperformed significantly
- Fine-tuning on domain data improved MRR by 34%
- Organization-specific terminology critical
- Acronym handling surprisingly important

**Enterprise integration is the hard part:**

- Connector development took 40% of project time
- Permission syncing was complex and critical
- Change management as important as technology
- Executive sponsorship essential for adoption

## Links

- [System Architecture](#)
- [User Guide](#)
- [API Documentation](#)
- [Evaluation Results](#)

