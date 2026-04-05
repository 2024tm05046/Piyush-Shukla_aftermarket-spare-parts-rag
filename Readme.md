                                                                                                                              **Aftermarket Spare Parts Multimodal RAG System**                                                                            
**Problem Statement**                                                                                                         
**Domain Identification**                                                                                                     
This project is situated in the domain of automotive aftermarket spare parts supply chain management, with a specific focus on inventory optimization for large-scale commercial vehicle enterprises. In this domain, organizations manage tens of thousands of spare part SKUs across multi‑tier distribution networks consisting of central distribution centers, regional warehouses, and service stations. Effective spare parts inventory management plays a critical role in customer service levels, asset uptime, and overall enterprise profitability.
**Problem Description**                                                                                                       
With the rapid expansion of China’s automotive aftermarket, spare parts inventory has emerged as a strategic challenge for vehicle manufacturers. Enterprises struggle to balance high service levels with rising inventory carrying costs due to factors such as heterogeneous demand patterns, long lead times, and extremely high SKU variety. Operational insights required for decision‑making are often buried within multimodal documents, including academic research papers, internal reports, and policy documents containing free text, analytical tables, formulas, and conceptual diagrams.
The dataset used in this project — “Research on Optimization Strategy of Aftermarket Spare Parts Inventory Management for Company F” — exemplifies this complexity. The document includes detailed explanations of existing inventory challenges, multiple tables defining classification rules, differentiated inventory strategies, and simulated performance results. Extracting actionable insights from such documents using traditional keyword search is inefficient, time‑consuming, and error‑prone.
**Why This Problem Is Unique**                                                                                                                                                                                          
Unlike generic document question‑answering tasks, this problem requires domain‑specific reasoning over structured and semi‑structured data. Queries often require interpreting relationships between spare parts classification matrices, inventory models such as (T,S) and (B,S), and quantitative performance metrics like service levels and fill rates. The presence of mathematical inventory logic, legacy classification rules, and simulation result tables makes this problem particularly unsuitable for basic text search or rule‑based retrieval systems.
**Why Retrieval‑Augmented Generation (RAG)**                                                                                                                                                                  
A Retrieval‑Augmented Generation (RAG) approach is well‑suited for this use case because it ensures responses are explicitly grounded in the source document. Fine‑tuning a language model would be costly, inflexible, and unsuitable for frequently updated operational documents. In contrast, RAG enables dynamic retrieval of relevant text, table, and image‑derived chunks at query time, ensuring explainable, traceable, and context‑aware answers. This is especially important in supply chain decision‑making, where hallucinated answers could lead to costly operational errors.
**Expected Outcomes**                                                                                                         
A successful system enables supply chain planners and inventory managers to:

Query spare parts classification logic and understand its impact on stocking policies.
Retrieve and interpret table‑based inventory strategies and service‑level rules.
Analyze simulation results comparing original and optimized inventory approaches.
Support inventory cost reduction and service‑level improvement decisions through grounded, explainable answers.

**Architecture Overview**                                                                                                     
<img width="4032" height="833" alt="Mermaid-preview" src="https://github.com/user-attachments/assets/699c1231-e8cd-476b-9fbc-af88e58fad55" />

**Sample Dataset**                                                                                                            
The system uses a domain‑specific research paper titled:
“Research on Optimization Strategy of Aftermarket Spare Parts Inventory Management for Company F”
The document contains:

Explanatory text describing inventory management challenges
Multiple tables defining spare parts classification rules
Differentiated inventory strategy matrices
Simulation results comparing original and optimized approaches
Conceptual diagrams illustrating inventory structure and strategy logic

This dataset is used to validate multimodal ingestion, retrieval, and grounded question‑answering across text, tables, and image‑derived summaries.

**Chunking Strategy**                                                                                                         
The dataset is processed using modality‑aware chunking:

Text chunks: Narrative sections such as problem descriptions, methodology, and conclusions are split by page and paragraph boundaries.
Table chunks: Each table (e.g., classification rules, inventory strategy matrices, simulation results) is extracted as a standalone chunk with preserved row‑column structure.
Image chunks: Diagrams and conceptual figures are summarized into concise textual descriptions using a vision‑language model (VLM) before embedding.

Each chunk is tagged with metadata including source filename, page number, and chunk type (text, table, image_summary).

**Technology Choices**                                                                                                        
Document Parsing: PyPDF for reliable extraction of academic‑style PDF text.
Embeddings: HuggingFace all‑MiniLM‑L6‑v2 for lightweight, efficient semantic retrieval.
Vector Store: FAISS for fast local similarity search.
LLM: Open‑weight or API‑based language model for answer generation.
Framework: LangChain for RAG pipeline orchestration.
API Layer: FastAPI for RESTful endpoints and interactive Swagger documentation.

**Setup Instructions**                                                                                                        
Clone the repository
Install dependencies
Run the FastAPI server
Open Swagger UI

**API Documentation**                                                                                                         
/health
Returns system status, uptime, and indexed document count.
/ingest
Processes the spare parts PDF, extracts multimodal chunks, embeds them, and stores them in the vector index.
/query
Accepts a natural‑language question and returns a grounded answer with source references (file name and page number).

**Screenshots**                                                                                                               
Screenshots demonstrating system functionality are provided in the screenshots/ folder:

Swagger UI
Successful PDF ingestion
Text‑based query
Table‑based query
Image/diagram‑based query
Health endpoint response

**Limitations & Future Work**                                                                                                 
Table extraction is limited to text‑based parsing; future versions may integrate structured table parsers.
Image understanding is dependent on the quality of diagram summarization.
Real‑time inventory data integration is outside the scope of this prototype.
Future work includes metadata‑based filtering and multi‑document reasoning.


