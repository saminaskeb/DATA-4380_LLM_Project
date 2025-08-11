# GPT, Just Tell Me What to Eat

* This repository contains an AI-powered meal planning assistant that takes user-input ingredients, generates vegan recipes, identifies missing ingredients, and fetches store URLs plus USDA nutrition information.

---

## Overview

The task is to create a flexible, budget-friendly meal planning tool that uses an LLM to generate recipes based on what the user already has.  
From the generated recipe, the system determines which ingredients are missing and then:

1. Uses a search engine API to find the best store URLs for those missing items.
2. Retrieves nutritional composition from the USDA FoodData Central API.

The approach integrates **natural language generation**, **ingredient parsing**, **store link retrieval**, and **nutrition data scraping** into a single automated workflow.

---

## Summary of Work Done

### Data

**Input:**
- List of pantry ingredients provided by the user (text input).
- USDA FoodData Central database for nutrition data.
- Store product search results (via Google Custom Search API).

**Output:**
- Vegan recipe text.
- Parsed ingredient list.
- Missing ingredient list with:
  - Store URL(s)
  - USDA nutritional data

**Data Size:**
- No large training dataset — this is an inference-only LLM application using live API queries.

---

#### Preprocessing / Clean-up
- Recipe text normalization to ensure ingredient parsing works reliably (line breaks before each “- ” and section header).
- Removal of truncated or incomplete instruction sections (optional mode).
- String cleaning to improve fuzzy matching between user pantry items and recipe ingredients.

---

#### Data Visualization
- N/A for now — could later add plots comparing macros of selected recipes or cost breakdown per meal.

---

### Problem Formulation

**Input:** List of ingredients from the user.  
**Output:** Recipe title, full ingredient list, missing ingredients with store URLs and USDA nutrition data.

**Model:**
- Base LLM (transformers) for recipe generation.
- Custom parsing and matching algorithms for ingredient list extraction.

**Loss / Optimizer:** N/A — this is an inference-only project.

---

### Training
- No model training performed — system relies on pre-trained LLM.
- Fine-tuning potential exists for recipe style/format consistency.

---

### Performance Comparison
- Performance is evaluated on:
  - Accuracy of ingredient parsing.
  - Relevance of store URLs.
  - Accuracy of USDA macro retrieval.
- Manual testing was used to verify outputs.

---

### Conclusions
- LLM-based recipe generation works well for diverse input ingredients.
- Ingredient parsing needed normalization for high accuracy.
- Real-time price fetching from major grocery sites was inconsistent due to anti-scraping measures — pivoted to store URL retrieval only.
- USDA API integration provides accurate, credible nutrition data.

---

### Future Work
- Integrate cost estimation by scraping prices where possible.
- Add recipe cost and nutrition optimization modes.
- Build a front-end interface for non-technical users.
- Add recipe image generation using an image model.

---

## How to Reproduce Results

**Steps:**
1. Clone the repository.
2. Install dependencies (see Software Setup).
3. Create a `.env` file with:
   - `GOOGLE_API_KEY` (Google Custom Search API)
   - `GOOGLE_CSE_ID` (Custom Search Engine ID)
   - `USDA_API_KEY` (USDA FoodData Central API key)
4. Run:
   ```bash
   python main.py
   ```
5. Enter your pantry items and see generated results.

---

### Overview of Files in Repository

- **main.py** → Main execution script for the workflow.
- **llm_recipe.py** → Generates recipe text using LLM.
- **ingredient_parser.py** → Parses ingredients from generated recipe.
- **store_search.py** → Queries Google CSE for store URLs.
- **usda_nutrition.py** → Retrieves nutrition data from USDA API.
- **utils.py** → Helper functions for string cleaning and fuzzy matching.
- **README.md** → Project documentation.

---

### Software Setup

**Required Packages:**
```bash
pip install transformers google-api-python-client fuzzywuzzy python-dotenv requests
```

---

### Data

- **USDA FoodData Central API** — [https://fdc.nal.usda.gov/api-guide.html](https://fdc.nal.usda.gov/api-guide.html)  
- **Google Custom Search API** — [https://developers.google.com/custom-search/v1/overview](https://developers.google.com/custom-search/v1/overview)

---

### Training
- No training required — inference-only.

---

#### Performance Evaluation
- Evaluate by running multiple ingredient inputs and verifying:
  - Recipe plausibility.
  - Correct missing ingredient detection.
  - Relevance of store URLs.
  - Accuracy of USDA macro data.

---

## Citations
- Devlin, J., et al. (2019). *BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding.*
- USDA FoodData Central. [https://fdc.nal.usda.gov](https://fdc.nal.usda.gov)
- Google Custom Search API. [https://developers.google.com/custom-search](https://developers.google.com/custom-search)
