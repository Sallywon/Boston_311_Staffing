# Staffing Boston's 311 City Service Teams

Month-by-month crew plan for four Boston 311 departments in 2025, with a GenAI intake assistant that classifies resident messages and warns when crews are short.

## Architecture
[Architecture diagram](architecture.png)

## Repository structure
- `data_forecast/`: data preparation, 2025 demand forecast, sensitivity analysis (Tatenda Mwashaireni)
- `intake/`: Intake Assistant (RAG + structured output), test sets, synthetic messages (Heewon)
- `staffing/`: staffing model and shortage check pipeline (Jongmin)

## Setup
1. Run the notebooks in Google Colab, in this order: data_forecast → intake → staffing.
2. Add `GOOGLE_API_KEY` to Colab Secrets.
3. Download the 2023 and 2024 311 data from Analyze Boston (https://data.boston.gov/dataset/311-service-requests). The raw files are not in this repo.
4. Put the CSV files from each folder in a Google Drive folder named `IE5374_311_project`.

## Demo video
(https://youtu.be/zO1dara2k44)

## Team contributions
**Tatenda Mwashaireni – Data Preparation, Demand Forecasting & Sensitivity Analysis**
- Cleaned and processed the Boston 311 service request datasets for 2023 and 2024 using Python and Pandas.
- Filtered and aggregated monthly service requests for four departments: Public Works (PWDx), Transportation (BTDT), Parks & Recreation (PARK), and Inspectional Services (ISD).
- Developed a monthly demand forecasting model for January–December 2025 using historical trends and seasonal patterns.
- Generated 48 monthly forecasts across the four departments, with a total estimated demand of **274,137 requests for 2025**.
- Performed sensitivity analysis using three scenarios: baseline demand, a 20% increase, and a 20% decrease.
- Created visualizations showing monthly demand forecasts by department and citywide sensitivity scenarios.
- Prepared department demand shares, request-type data, and CSV outputs for integration with the Intake Assistant and staffing model.
- Developed and executed a Jupyter Notebook containing the data preparation, forecasting, sensitivity analysis, and visualizations.

**Heewon – Intake Assistant**
- Built the request type catalog(top 40 of 158 types, about 95% of requests) with plain-language descriptions
- Built the Intake Assistant with RAG(embedding retrieval), structured output (Gemini JSON schema), and prompt engineering (department descriptions and classification rules), including "Other" and "Unknown" handling and follow-up questions
- Created and reviewed two test sets 49 and 38 messages) and evaluated accuracy(type 94.7%, department 100% on new messages)
- Generated synthetic August message streams (normal and parking surge) and handed off extra requests per department to the pipeline
- Analyzed employee vs. resident requests (Other considerations) and built the demo UI(Gradio)
- Set up the GitHub repository
- produced the demo video

**Jongmin – Staffing Model & Pipeline**
- Designed the staffing cost structure (crew pay including the paid training month, Parks seasonal crews, release fees, and overdue costs of $20 plus $100 for requests 30+ days late) and the modeling assumptions the brief leaves open (first-in-first-out backlog, one-month targets, hiring and release timing, fixed January crews).
- Built a month-by-month plan simulator that tracks backlog, overdue requests, utilization and cost for any crew plan, with a validation step that checks each plan against the brief's hiring, release and seasonal-crew rules.
- Defined the staffing policy: plan for forecast demand plus a 10% buffer and carried-over backlog, keep crews needed again within 4 months (based on the release-vs-keep break-even), and cover the Parks peak with seasonal crews only (based on the seasonal-vs-regular break-even).
- Produced the 2025 month-by-month crew plan by department, including hiring and release timing ($16.85M total cost, 99.8% on-time rate on the forecast).
- Ran sensitivity analysis
