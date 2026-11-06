# Staffing Boston's 311 City Service Teams

Month-by-month crew plan for four Boston 311 departments in 2025, with a GenAI intake assistant that classifies resident messages and warns when crews are short.

## Architecture
(team architecture diagram here)

## Repository structure
- `data_forecast/`: data preparation, 2025 demand forecast, sensitivity analysis (Tez)
- `intake/`: Intake Assistant (RAG + structured output), test sets, synthetic messages (Heewon)
- `staffing/`: staffing model and shortage check pipeline (Jongmin)

## Setup
1. Run the notebooks in Google Colab, in this order: data_forecast → intake → staffing.
2. Add `GOOGLE_API_KEY` to Colab Secrets.
3. Download the 2023 and 2024 311 data from Analyze Boston (https://data.boston.gov/dataset/311-service-requests). The raw files are not in this repo.
4. Put the CSV files from each folder in a Google Drive folder named `IE5374_311_project`.

## Demo video
(link here)

## Team contributions
**Tez – Data & Forecast**
- (to be added)

**Heewon – Intake Assistant**
- Built the request type catalog (top 40 of 158 types, about 95% of requests) with plain-language descriptions
- Built the Intake Assistant: embedding retrieval (RAG) + Gemini structured output, with “Other” and “Unknown” handling and follow-up questions
- Created and reviewed two test sets (49 and 38 messages) and evaluated accuracy (type 94.7%, department 100% on new messages)
- Generated synthetic August message streams (normal and parking surge) and handed off extra requests per department to the pipeline
- Analyzed employee vs. resident requests (Other considerations) and built the demo UI (Gradio)
Produced the demo video

**Jongmin – Staffing Model & Pipeline**
- (to be added)
