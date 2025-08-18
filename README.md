# ACLED Conflict Event Extraction with NLP

## Overview

As part of my final Master's research project, this repository presents a natural language processing pipeline for extracting structured data from unstructured conflict event narratives in the ACLED dataset. The system maps raw text to a 14-field JSON schema and supports instruction-based fine-tuning of a compact language model (Llama 3.2 1B) using LoRA, executed fully on-device via MLX for Apple Silicon, for total privacy. This work is grounded in the context of contemporary European security, with a particular focus on the Ukraine–Russia conflict and broader regional dynamics across Eastern and Central Europe, along with the Baltic states.

## Features

- 14-field extraction covering time, place, actors, and impacts  
- Cross-border attribution for interstate operations  
- Quality scoring on a ten-point scale for note clarity and density  
- MLX support on Apple Silicon using quantised weights and LoRA adapters  
- Validation suite with targeted unit tests and a stratified evaluation set 

## Repository structure

- Data_Analysis_CEB.ipynb: Data quality, geography, scoring, temporal trends
- Data_Filtering_Export.ipynb: Pattern-based extraction, validation, dataset export
- Model_Fine_Tuning.ipynb: MLX + LoRA fine-tuning and evaluation

## Data

- **Source:** ACLED (Europe–Central Asia, 2018–2025)  
- **Total events processed:** 309,974  
- **Basic filtering pass rate:** 89.3% (276,856 notes)  
- **High-quality subset:** 78.8% scoring ≥ 6/10
- **Geography:** Ukraine, Russia, Belarus, Moldova, Bulgaria, Romania, Poland, Czech Republic, Hungary, Slovakia, Lithuania, Latvia, Estonia  

## Model and Training

- **Base model:** Llama 3.2 Instruct, 1B, 4-bit  
- **LoRA config:** rank 16, alpha 32, dropout 0.1  
- **Platform:** Apple Silicon with MLX (on device, offline)  
- **Training signal:** JSON-formatted instruction–response pairs exported by the pipeline  

## Typical Workflow

1. **Analyse data** – `Data_Analysis_CEB.ipynb`  
   Assess geographic distribution, scoring, and temporal trends.  
2. **Extract and export** – `Data_Filtering_Export.ipynb`  
   Apply rules, validate output, export training JSONL and test CSV (with metadata).  
3. **Fine-tune and evaluate** – `Model_Fine_Tuning.ipynb`  
   Configure LoRA adapters, train with MLX, evaluate performance, and save adapters.

## Licensing and Ethics

- ACLED data is **not redistributed** in this repository due to licensing.  
  Please obtain data directly from [ACLED](https://acleddata.com).  
- Outputs are intended for academic analysis and research tooling.  
  This is **not** an operational intelligence product.

## Credits

- **[ACLED](https://acleddata.com/)** – Armed Conflict Location & Event Data Project. This work uses ACLED's publicly available data to study regional conflict patterns.  
- **[MLX](https://github.com/ml-explore/mlx)** – Apple's MLX framework for training models efficiently on Apple Silicon hardware.  
- **[Llama 3](https://huggingface.co/mlx-community/Llama-3.2-1B-Instruct-4bit)** – Meta's Llama 3.2 1B instruction-tuned model used here under its open model licence and hosted weights.