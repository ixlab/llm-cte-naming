# llm-cte-naming
A repository containing work done on evaluating large language models (LLM) at naming SQL common table expressions (CTEs).


### Requirements

To run this code, you will need:
- a huggingface token in your environment, preferably in a `.env` file.
- a github token in your environment, preferably in a `.env` file

### Contents

The code contains the following datasets in `data_files/`:
- `github_ctes.json`
    - this is a dataset of scraped github CTEs, the querying done on github is not deterministic since repos can be added/deleted, so the dataset was simply preserved for replication.
- `curated_ctes.jon`
    - this is a set of hand curated ctes from `github_ctes.json` that has been used for LLM name evaluation and name generation.
- `spider2-lite-ctes.json`
    - This has CTEs extracted from the spider2-lite dataset found here: https://github.com/xlang-ai/Spider2/tree/main/spider2-lite


The code contians the following executables in `notebooks`:
- `01_scrape-ctes-from-github.ipynb`
    - This notebook walks through the process of generating `github_ctes.json`.
- `02_generate-summaries.ipynb`
    - This notebook walks prompts LLMs to generate summaries of CTEs given SQL code.
- `03_calculate_phrase_similarity.ipynb`
    - This notebook walks through the process of embedding the names and summaries and calculating phrase_similarity, the cosine similarity between a CTE name and its summary phrase.
- `04_1_poll_gpt.ipynb`
    - This notebook polls the OpenAI gpt models via the `openai` API and asks for their judgement on given CTE names.
- `04_2_poll-llms.ipynb`
    - This notebook polls the open source LLMs via huggingface and asks for their judgement on given CTE names.
- `05_graph_similarities.ipynb`
    - This notebook compares phrase_similarity distributions across original and LLM generated names for both the github curated and spider-2-lite CTE datasets.
- `06_scatter_plots_refactored.ipynb`
    - This notebook shows scatterplot graphs that compare phrase_similarity values with polled LLM judgements (and manual curated judgements in the curated dataset) for CTE names.