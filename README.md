# Predictive Analytics for Multi-modal Documents and Time Series Data

## Problem Definition

**Objective:** Develop a predictive analytics system that integrates multi-modal documents (text, tables, images) with time series data to forecast future events and generate comprehensive reports.

**Scope:**
- **Prediction Types:**
  - **Binary classification**: Will event X will occur? (Y/N)
  - **Open-ended event discovery:** The system identifies potential future events or outcomes without predefined classes(What events would happen?)
  - **Scenario generation:** Creating multiple plausible future narratives with probability estimates

## Potential Applications

### Financial Forecasting
- Discovering unforeseen market shifts by analyzing annual reports, news, and price patterns
- Forecasting company default risk by analyzing financial statements, audit reports, and market signals
- Generating potential business evolution scenarios beyond simple "default/no default"

### Business Intelligence
- Uncovering emerging customer segments and behaviors not previously categorized
- Predicting the effectiveness and ROI of promotion strategies across different channels
- Forecasting demand volatility and supply chain impacts based on market signals

### Risk Management
- Generating potential crisis scenarios not observed in historical data
- Generating comprehensive risk reports with mitigation strategies and impact assessments
- Identifying complex interdependencies between seemingly unrelated risk factors

## Technical Approach

### 1. Document Layout Detection
Document Layout detection algorithm and OCR tools will be used to extract text, table, etc. from documents. 
Input: Documents
Output: Texts, tables
Document Layout Detection Methods: 
  - LayoutLMv3: https://arxiv.org/pdf/2204.08387
  - YoLo: https://arxiv.org/abs/1506.02640

OCR Methods:
  - Tesseract-ocr: https://github.com/tesseract-ocr/tesseract
  - PaddleOCR: https://github.com/PaddlePaddle/PaddleOCR

### 2. Event Extraction
This module aims to extract events from mutimodal data. An event will have a triger(action) and several mentions(arguments) including time, location, participants. For time-series and tabular data, anmoly activities can be treated as events.
Input: Text, Table, Time Series data
Output: Events
**Event Extraction From Text:**
  - A Survey of Event Extraction From Text
  - Event Extraction as Dependency Parsing
    
**Event Extraction(Anomaly Detection) From Tabular:**
  - Anomaly Detection of Tabular Data Using LLMs
    
**Event Extraction From Time-Series:**
  - Event Detection via Probability Density Function Regression
    
**Multimodal Event Detection:**
  - A survey of multimodal event detection based on data fusion: https://link.springer.com/article/10.1007/s00778-024-00878-5

### 3. Event Representation
This module aims to represents events in a chain or knowledge graph. The relation could be temporal or causal.
In this process, causal relations will be identified.
Input: Events
Output: Event Chain or Knowledge Graph 
**Event Chain:** 
  - Time: Unsupervised Event Chain Mining from Multiple Documents
  - Causality: Event Story Line
**Event Knowledge Graph or Event Evolutionary GraphEvolution:**
  - Constructing Narrative Event Evolutionary Graph for Script Event Prediction
  
### 4. Event Prediction
This module aims to predict future events given event chains, event knowledge graphs or event causal knowledge graphs.

Input: Event chains or knowledge Graph 

Output: Predict Events



