# LLM-Based Coding of Student Causal Diagrams

This repository contains code and resources from a study exploring the use of Large Language Models (LLMs) to code students' causal diagrams. The project evaluates how effectively LLMs can automate the coding process traditionally done by human researchers, comparing different prompting strategies and model configurations.

## Project Overview

Causal diagrams are visual representations that students create to demonstrate their understanding of cause-and-effect relationships in texts. Coding these diagrams is typically a manual, time-consuming process performed by researchers and teachers.

This project:
- Evaluates how accurately LLMs can code student causal diagrams
- Compares different prompting strategies and model configurations
- Analyzes performance metrics for extraction and position coding
- Provides cost analysis for different LLM implementations

## Repository Structure

The repository is organized as follows:

- **Batch Input Files**: Contains JSONL files with batch requests to the OpenAI API
- **Batch Response Files**: Stores the responses from the OpenAI batch API
- **Data**: Contains the dataset of student causal diagrams
- **Prompts**: Contains different prompting strategies for the LLMs
- **Texts**: Contains the original texts students analyzed when creating diagrams
- **documentation**: Stores analysis results and performance metrics

## Key Scripts

The repository includes several Python scripts for analyzing and processing data:

- **batch_request.py**: Creates and submits batch requests to OpenAI
- **batch_retrieve.py**: Downloads completed batch results
- **batch_process.py**: Processes responses and calculates performance metrics
- **explore_results.py**: Compares results across different settings
- **explore_dataset.py**: Provides descriptive statistics about the dataset

## Prerequisites

Before using this code, you'll need:

- Python 3.8 or higher
- An OpenAI API key with access to GPT-4o models
- The following Python packages: pandas, numpy, openai, pydantic, json

## Usage Guide

### Step 1: Create and Submit Batch Requests

Run the `batch_request.py` script to create a batch request:

```bash
python batch_request.py
```

This script will:
1. Ask you to select a prompting strategy from predefined settings
2. Request the number of diagrams you want to analyze
3. Ask you to choose an LLM model (GPT-4o or GPT-4o-mini)
4. Create a JSONL file with the batch request in the "Batch Input Files" folder
5. Optionally upload and submit the batch to OpenAI

Make sure to:
- Add your OpenAI API key in the appropriate place in the script
- Update the data file path in the script to point to your data file

### Step 2: Retrieve Batch Responses

Once your batch request has been processed by OpenAI, run:

```bash
python batch_retrieve.py
```

This script will:
1. Connect to your OpenAI account and show your recent batch requests
2. Display the status of each batch (active, completed, or failed)
3. Allow you to select which completed batches to download
4. Save the responses to the "Batch Response Files" folder

### Step 3: Process and Analyze Results

After retrieving the responses, analyze the results:

```bash
python batch_process.py
```

You'll be prompted to enter the name of the batch response file to process. The script will:
1. Load the batch responses and the original human coding
2. Compare the LLM's coding with the human coding
3. Calculate performance metrics for both extraction and position coding:
   - Accuracy, Precision, Recall, F1 score
   - Cohen's kappa
   - Confusion matrices (TP, FP, TN, FN)
4. Calculate token usage and associated costs
5. Generate an Excel file with the results in the "documentation" folder

### Step 4: Compare Different Strategies

To compare results across different settings:

```bash
python explore_results.py
```

Before running this script:
- Edit the script to specify which result files to include in your analysis
- Add the relevant file names to the `settings` list in the script

The script will generate a comprehensive Excel file comparing all specified settings.

## Understanding the Analysis

### Coding Tasks

The system evaluates two main coding tasks:

1. **Extraction Coding**: Distinguishing between "g" ("good" for correct responses) and "c" ("commission" for errors of commission) elements in student diagrams
2. **Position Coding**: Determining the correct positioning or relationships between elements

### Prompting Strategies

Various prompting strategies can be tested, including:

- **With/Without Truth Values**: Whether to include ground truth in the model diagrams
- **Number of Examples**: Varying from 0 to 50 examples in the prompt
- **Diagram Creation**: Whether to include diagram creation instructions

### Performance Metrics

The analysis calculates several metrics:

- **Accuracy**: Overall correctness of the LLM's coding
- **Precision**: How many of the LLM's positive identifications were correct
- **Recall**: How many actual positives were identified by the LLM
- **F1 Score**: Harmonic mean of precision and recall
- **Cohen's Kappa**: Agreement between human and LLM coding beyond chance

### Cost Analysis

The system tracks token usage and costs for different:
- Model variants (e.g., GPT-4o vs. GPT-4o-mini)
- Prompting strategies
- Number of diagrams

## Example Workflow

A typical workflow might look like:

1. Run `batch_request.py` and select "V1.1_woTruth_5Examples_allUserPrompt" as the strategy, 20 as the number of diagrams, and "gpt-4o-2024-08-06" as the model
2. Wait for the batch to complete (this may take several minutes to hours)
3. Run `batch_retrieve.py` and select the completed batch to download
4. Run `batch_process.py` and enter the batch file name to analyze the results
5. Review the Excel file in the "documentation" folder to see the performance metrics
6. Repeat with different strategies or models to compare performance
7. Use `explore_results.py` to create a comprehensive comparison

## Modifying the Code

If you need to adapt this code for your own dataset:
- Update the data loading and filtering functions in each script
- Modify the data structure in model_diagrams.json to match your diagram format
- Adjust the prompts in the "Prompts" folder to fit your specific coding task

## License

See the LICENSE file for license information for this project


## Contact

niklas.wenzel@maastrichtuniversity.nl

---

*Note: This repository is part of a research study on using LLMs for coding student work. For more information about the research methodology and findings, please refer to the associated publication.*