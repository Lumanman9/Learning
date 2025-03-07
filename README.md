# Predictive Analytics for Multi-modal Documents and Time Series Data

## Problem Definition

**Objective:** Develop a predictive analytics system that integrates multi-modal documents (text, tables) with time series data to forecast future events and generate comprehensive reports.

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

## Current Approach 
- Infusion during dembedding
- Infusion through cross-attention
- Infusion through voting

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
  - A Survey of Event Extraction From Text: https://www.researchgate.net/publication/337638438_A_Survey_of_Event_Extraction_From_Text
  - Event Extraction as Dependency Parsing: https://aclanthology.org/P11-1163/
    
**Event Extraction(Anomaly Detection) From Tabular:**
  - Anomaly Detection of Tabular Data Using LLMs: https://arxiv.org/abs/2406.16308
    
**Event Extraction From Time-Series:**
  - Event Detection via Probability Density Function Regression: https://arxiv.org/abs/2408.12792
    
**Multimodal Event Detection:**
  - A survey of multimodal event detection based on data fusion: https://link.springer.com/article/10.1007/s00778-024-00878-5

### 3. Causal Relation Extraction
**Causal Relation Identification from text:**

Input: Text and event pairs

Output: Wether two events have causal relation

  - Rule-based: explicit, using words like 'because', 'lead to'.
    a. Automatic Extraction of Cause-Effect Information from Newspaper Text Without Knowledge-based Inferencing https://academic.oup.com/dsh/article-abstract/13/4/177/928333?redirectedFrom=fulltext
  - Knowledge graph based: KEPT: Knowledge Enhanced Prompt Tuning for event causality identification https://dl.acm.org/doi/abs/10.1016/j.knosys.2022.110064
  - Prompt based: Event Causality Identification via Derivative Prompt Joint Learning: https://aclanthology.org/2022.coling-1.200/
  - Diffusion based: 

**Causal Relation Extraction from historical data:**

Input: historical data with varibles 

Output: Wethter two varibles have causal relation and consturct the causal graph

  - Constraint based using Conditional Independence Tests: PC algorithm/ Fast Causal Inference (FCI) algorithm
  - Bayesian score-based using a greedy approach to optimize a scoring function: Greedy Equivalence Search (GES) algorithm
  - Granger Causality(Time-Series)
  - LLM based:
     a. Can Large Language Models Distinguish Cause from Effect?
     b. From Query Tools to Causal Architects: Harnessing Large Language Models for
Advanced Causal Discovery from Data
     c. Integrating Large Language Models in Causal Discovery
     d. Large Language Models are Effective Priors for Causal Graph Discovery
     e. EFFICIENT CAUSAL GRAPH DISCOVERY USING LARGE LANGUAGE MODELS
     f. Zero-shot Causal Graph Extrapolation from Text via LLMs
  - Others:
     a. Additive Noise Models (ANMs): https://arxiv.org/abs/2110.08087
     b. LiNGAM (Linear Non-Gaussian Acyclic Model): https://jmlr.org/papers/volume7/shimizu06a/shimizu06a.pdf
     c. Constrained Nonlinear Independent Component Analysis (ICA): https://pdf.sciencedirectassets.com/776857
     d. Linear Non-Gaussian Latent Variable Model with Generalized Independent Noise Condition (LiNGLaM-GIN): https://arxiv.org/abs/2010.04917
     e. Best Order Score Search (BOSS) Algorithm

    


### 4. Event Representation
This module aims to represents events in a chain or knowledge graph. The relation could be temporal or causal.
In this process, causal relations will be identified.

Input: Events

Output: Event Chain or Knowledge Graph 

**Event Chain:** 
  - Time: Unsupervised Event Chain Mining from Multiple Documents https://dl.acm.org/doi/abs/10.1145/3543507.3583295
  - Causality:
    a. Event Story Line https://aclanthology.org/W17-2711/
    b. Causal prediction of top-k event types over real-time event streams https://arxiv.org/abs/1508.06976
**Event Knowledge Graph or Event Evolutionary GraphEvolution:**
  - Constructing Narrative Event Evolutionary Graph for Script Event Prediction: https://arxiv.org/abs/1805.05081

### 5. Alignment
This module aims to align elements between knowledge graphs or ontologies.

Input: An event and a causal knowledge graph

Output: A concept in causal knowledge graph

  - Entity to Knowledge Graph:
    a. Improving Knowledge Graph Entity Alignment with Graph Augmentation https://arxiv.org/abs/2304.14585
    b. AutoAlign: Fully Automatic and Effective Knowledge Graph Alignment enabled by Large Language Models https://arxiv.org/abs/2307.11772
  - Ontology anligment:
    a. Ontology alignment with semantic and structural embeddings: https://www.sciencedirect.com/science/article/abs/pii/S1570826823000276
    
  
### 6. Event Prediction
This module aims to predict future events given event chains, event knowledge graphs or event causal knowledge graphs.

Input: Event chains or causal knowledge Graph with event queries

Output: Predict Events

 - Predicting an Effect Event from a New Cause Event Using a Semantic Web Based Abstraction Tree of Past Cause-Effect Event Pairs: https://ceur-ws.org/Vol-2029/paper19.pdf
 - Real-time Top-K Predictive Query Processing over Event Streams: https://arxiv.org/abs/1508.06976
 - Event prediction based on causality reasonin: https://link.springer.com/chapter/10.1007/978-3-030-14799-0_14
 - Learning causality for news events prediction: https://dl.acm.org/doi/10.1145/2187836.2187958
 - Using external knowledge for financial event prediction based on graph neural networks: https://dl.acm.org/doi/10.1145/3357384.3358156
 - Event Prediction in the Big Data Era: A Systematic Survey: https://dl.acm.org/doi/pdf/10.1145/3450287
   






