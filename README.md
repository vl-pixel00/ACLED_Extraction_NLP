# ACLED Conflict Event Extraction Using Natural Language Processing

## Abstract

This repository contains the implementation of my master's dissertation project investigating the application of natural language processing techniques for automated conflict event extraction from ACLED (Armed Conflict Location & Event Data Project) narratives. The research explores the efficacy of fine-tuned large language models in structured data extraction from unstructured conflict reporting, with a specific focus on Eastern Europe, Central Europe, and the Baltic States.

**Base Model**: Llama 3.2 1B Instruct (4-bit quantised), Apple's MLX framework, and ACLED's conflict database.

## Research Objectives

- **Primary Objective**: Develop an automated pipeline for extracting structured conflict event data from unstructured ACLED narratives using state-of-the-art NLP techniques
- **Secondary Objectives**: 
  - Evaluate the performance of quantised large language models on resource-constrained hardware
  - Implement quality assessment mechanisms for narrative clarity and information density
  - Create a reproducible methodology for conflict event data processing
  - Analyse geographical and temporal patterns in conflict data quality

## Methodology

### Data Processing Pipeline
The research employs a multi-stage approach combining rule-based filtering with machine learning-based extraction:

1. **Data Quality Assessment**: Ten-point scoring system evaluating structural indicators, information density, and content coherence
2. **Pattern-Based Extraction**: Field extraction system using pattern recognition for temporal, geographic, and actor intelligence
3. **Model Fine-Tuning**: Custom adaptation of Llama 3.2 1B Instruct (4-bit quantised) using LoRA (Low-Rank Adaptation) techniques
4. **Validation & Evaluation**: Multi-stage validation ensuring data integrity through field completeness and consistency checks

### Technical Architecture
- **Base Model**: Llama 3.2 1B Instruct (4-bit quantised) from [mlx-community/Llama-3.2-1B-Instruct-4bit](https://huggingface.co/mlx-community/Llama-3.2-1B-Instruct-4bit)
- **Fine-Tuning Method**: LoRA adapters (rank 16, alpha 32, dropout 0.1)
- **Platform**: Apple Silicon optimised using MLX framework with Metal backend
- **Output Format**: 14-field structured extraction covering temporal, spatial, actor, and impact dimensions

## Geographic Scope

The pipeline processes ACLED records from thirteen European countries:

- **Eastern Europe**: Ukraine, Russia, Belarus, Moldova, Bulgaria, Romania
- **Central Europe**: Poland, Czech Republic, Hungary, Slovakia  
- **Baltic States**: Lithuania, Latvia, Estonia

This geographic constraint ensures regional coherence whilst concentrating analysis on areas experiencing significant security developments, particularly interstate conflict and cross-border operations.

## Extracted Fields

The pipeline extracts fourteen structured elements:
- **Temporal Intelligence**: Multi-format date parsing and time specifications
- **Geographic Data**: Location hierarchy and cross-border operation handling
- **Actor Detection**: 10-tier hierarchical system covering military forces, protest groups, and security services
- **Modern Weapons Recognition**: Contemporary systems including FPV drones, Shahed drones, HIMARS, and calibre-specific artillery
- **Infrastructure Impact**: Eight critical categories from power grid disruption to military installations
- **Cross-Border Intelligence**: Special handling for interstate operations with automatic attribution
- **Quality Metrics**: Content quality scoring and information density assessment

## Repository Structure

```
├── Data_Analysis_CEB.ipynb          # Data profiling, quality scoring, and country-level analysis
├── Data_Filtering_Export.ipynb      # Data processing pipeline and field extraction system
├── Model_Fine_Tuning.ipynb          # MLX-based model fine-tuning using LoRA adapters
├── README.md                        # Project documentation
├── requirements.txt                 # MLX environment dependencies
```

### Notebook Descriptions

#### Data_Analysis_CEB.ipynb

Data quality analysis and feasibility assessment covering:

- Geographic distribution patterns across 13 countries (Ukraine 78.6%, Russia 12.7%, others 8.7%)
- Quality assessment using conservative filtering criteria (89.3% pass rate (309,974) from 527,211 records)
- Detailed 10-point scoring system analysis (6.4/10 average quality across all countries)
- Temporal patterns and peak activity identification (2024: 71,030 quality notes)
- Research feasibility validation for machine learning applications
- Country-level quality statistics with pass rates ranging from 98.0% (Ukraine) to 9.0% (Bulgaria)
- Regional distribution analysis across Eastern Europe (95.7%), Central Europe (3.9%), and Baltic States (0.4%)

#### Data_Filtering_Export.ipynb

Core data processing pipeline featuring:

- Quality assessment framework with a 10-point scoring system
- Advanced field extraction system with pattern recognition
- Cross-border intelligence handling for interstate operations
- Multi-stage validation ensuring data integrity
- Geographic and actor consistency checks
- Export functionality for training datasets (JSONL format)

#### Model_Fine_Tuning.ipynb

Machine learning implementation covering:

- LoRA adapter configuration for Llama 3.2 1B Instruct (4-bit quantised) model
- MLX-optimised training procedures for Apple Silicon using Metal backend
- Fine-tuning workflow with structured accuracy metrics
- Model evaluation and adapter serialisation

## Technical Implementation

### Hardware Requirements
- **Recommended**: Apple Silicon Mac (M1/M2/M3/M4) with ≥16GB unified memory
- **Minimum**: 16GB system RAM

### Software Dependencies
- Python 3.11.3
- MLX framework with Metal backend (Apple Silicon)
- mlx_lm for model loading and fine-tuning workflows
- Pandas, NumPy for data manipulation
- Standard libraries: os, re, json, pathlib, etc.

## Installation

1. **Clone repository**:
   ```bash
   git clone [your-repo-url]
   cd ACLED_Extraction_NLP

2. **Install dependencies**:
    ```bash
    pip install -r requirements.txt

3. **Verify MLX installation (Apple Silicon only)**:
    ```bash
    import mlx.core as mx
    print(f"MLX version: {mx.__version__}")

## Research Significance

This work contributes to computational linguistics and conflict studies by:

1. **Methodological Innovation**: Demonstrating quantised LLM application for structured information extraction in conflict research
2. **Technical Contribution**: Providing a reproducible pipeline for ACLED data processing on consumer hardware
3. **Academic Value**: Offering insights into conflict event narrative quality and characteristics
4. **Practical Application**: Creating tools for automated conflict data analysis, focusing on modern warfare patterns

## Validation Results

The test suite validation achieved:

- **100% individual field accuracy** across 36 specific tests
- **Field completeness verification** across all fourteen target fields
- **Geographic and actor consistency** checks passed
- **Numeric range validation** for casualty figures implemented

## Performance Metrics

### Model Training Results
- Final training loss: 0.262
- Final validation loss: 0.255
- Field extraction success: 62.0% average completion
- JSON format compliance: 100% (400/400 responses)
- Core field accuracy: 99.2% (event_date, country, location, event_type)

### Data Quality Assessment
- Total records processed: 309,974
- Quality filtering pass rate: 89.3%
- High-quality subset (≥6/10): 78.8%
- Geographic coverage: 100% across 13 countries

## Ethical Considerations and Limitations

### Data Ethics
- **Source Attribution**: All data originates from ACLED's publicly available datasets
- **Usage Scope**: Research is strictly academic and non-operational
- **Privacy**: No personally identifiable information is processed or stored
- **Bias Mitigation**: Acknowledgement of potential reporting biases in source material

### Technical Limitations
- **Geographic Scope**: Analysis limited to thirteen European countries
- **Temporal Constraints**: Training data bounded by ACLED's reporting timeline
- **Model Constraints**: Performance limited by quantisation and 1B parameter count
- **Language Limitations**: Processing primarily English-language narratives

## Data Access and Licensing

**Important Notice**: This repository does **not** include the underlying ACLED dataset due to licensing restrictions. Researchers must:

1. Register with [ACLED](https://acleddata.com) for data access
2. Comply with ACLED's terms of use and attribution requirements
3. Acknowledge ACLED in any publications or presentations
4. Respect the non-commercial academic use limitations

## Academic Context

This project forms part of my Master's dissertation investigating modern conflict patterns through automated analysis techniques. The work was conducted during the academic year 2024-2025.

## Acknowledgements and Credits

I extend my gratitude to the organisations and research projects whose contributions made this research possible:

### ACLED (Armed Conflict Location & Event Data Project)
- **Contribution**: Providing a real-time conflict database with a rigorous data collection methodology
- **Impact**: ACLED's extensive geographical coverage forms the foundation of this research
- **Recognition**: ACLED's commitment to open data access enables academic research projects worldwide
- **Website**: [acleddata.com](https://acleddata.com)
- **Note**: All conflict event data used in this project originates from ACLED's publicly available datasets

### Llama 3.2 1B Instruct (4-bit quantised)
- **Model Source**: [mlx-community/Llama-3.2-1B-Instruct-4bit](https://huggingface.co/mlx-community/Llama-3.2-1B-Instruct-4bit)
- **Contribution**: Quantised language model optimised for instruction following and structured output generation
- **Technical Innovation**: Enabling high-quality natural language processing on consumer hardware through 4-bit quantisation
- **Implementation**: Fine-tuned using LoRA adapters for conflict event extraction tasks

### Apple MLX (Machine Learning Research Framework)
- **Contribution**: Efficient machine learning framework optimised for Apple Silicon
- **Technical Impact**: Enabling on-device model fine-tuning with unified memory architecture and Metal backend
- **Performance**: MLX's NumPy-like API and automatic differentiation enabled rapid prototyping
- **Innovation**: Memory-efficient training approach for consumer hardware
- **Documentation**: [ml-explore.github.io/mlx](https://ml-explore.github.io/mlx/)
- **Repository**: [github.com/ml-explore/mlx](https://github.com/ml-explore/mlx)

---

**Disclaimer**: This research is conducted for academic purposes only. The findings and methodologies presented are not intended for operational intelligence or policy-making applications. Users should exercise appropriate caution when interpreting conflict-related data and analyses.

**Third-Party Acknowledgement**: This project builds upon the work of ACLED, the Llama model developers, and Apple's MLX team. All trademarks and intellectual property rights remain with their respective owners.