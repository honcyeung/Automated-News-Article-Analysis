# Automated News Analysis with Gemini AI
This project demonstrates a complete, end-to-end data engineering pipeline that automates the process of fetching news articles, enriching them with AI-generated insights using the Google Gemini API, and storing them in a vector database for advanced querying and analysis.

The entire workflow is encapsulated within a single Jupyter Notebook, showcasing a streamlined process from raw data ingestion to an AI-ready dataset.

## Project Workflow
The pipeline follows a modern ETL (Extract, Transform, Load) process, enhanced with AI capabilities at its core. The diagram below illustrates the flow of data from raw sources to the final, queryable vector database.

```text
graph TD
    A[Start: RSS Feeds] --> B[Fetch New Articles];
    B --> C[Scrape Full Article Text];
    C --> D[AI Enrichment];
    subgraph D [AI Enrichment]
        D1[Summarize Article]
        D2[Categorize Article]
        D3[Generate Embeddings]
    end
    D --> E[Load to PostgreSQL];
    E --> F[End: Enriched Data in DB];
```

## Architecture Breakdown
- Extract: The pipeline begins by fetching the latest article metadata from specified RSS feeds (e.g., BBC News).

- Scrape: For each new article, it uses the Newspaper3k library to visit the article's URL and scrape the full text content, ensuring a high-quality dataset for analysis.

- Transform (AI Enrichment): This is the core of the project. For each article, the pipeline makes several calls to the Google Gemini API:

  - Summarization: Generates a concise, 2-3 bullet point summary of the article.

  - Categorization: Classifies the article into a predefined category (e.g., Technology, Politics, Science).

  - Embedding: Converts the entire article content into a 768-dimension vector embedding using the text-embedding-004 model. This embedding captures the semantic meaning of the text and is crucial for semantic search and RAG applications.

- Load: The final enriched data, including the original content, metadata, and all AI-generated insights, is loaded into a PostgreSQL database equipped with the pgvector extension. The script uses an "upsert" operation to efficiently insert new articles or update existing ones.

## Technology Stack
This project utilizes a modern, robust stack perfect for AI-powered data engineering tasks.

- Language: Python 3.9+

- AI & Machine Learning:

  - Google Gemini API: For summarization, classification, and state-of-the-art text embeddings.

  - Jupyter Notebook: For interactive development and showcasing the entire workflow.

- Data Ingestion & Processing:

  - feedparser: For reliable parsing of RSS feeds.

  - Newspaper3k: For web scraping and extraction of clean article text.

  - dotenv: For secure management of API keys.

- Database & Storage:

  - PostgreSQL: A powerful, open-source object-relational database.

  - pgvector: A PostgreSQL extension for storing and querying vector embeddings.

  - SQLAlchemy: A Python SQL toolkit and Object Relational Mapper (ORM) for interacting with the database.
