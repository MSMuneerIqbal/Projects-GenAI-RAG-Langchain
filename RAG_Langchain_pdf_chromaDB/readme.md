# FAQ Bot University - Google Colab Notebook

## Overview

This Google Colab notebook demonstrates a simple FAQ bot that utilizes a CSV file containing frequently asked questions and their corresponding answers. The primary focus is on extracting and displaying information based on user queries.

## Contents

The notebook includes:

- **Data Source**: A CSV file (`faq_bot_university.csv`) containing questions and answers related to university admissions.
- **Functionality**: 
  - Load the CSV data.
  - Process and display relevant information based on user input.
  
## Parameters

The following parameters and components are utilized in this project:

- **Google API Key**: Required for accessing Google services (e.g., Google Cloud Storage, Natural Language API).
- **Chroma DB**: Used as the vector database to store and retrieve vector embeddings.
- **Vector Embeddings Models**: Models used to convert text data into vector representations for efficient similarity search.
- **CSV File**: Contains the dataset of questions and answers (`faq_bot_university.csv`).

## Data

The data is sourced from a CSV file with the following structure:

| Row | Question                          | Answer                          |
|-----|-----------------------------------|---------------------------------|
| 1   | When is the admission deadline?   | The admission deadline is April 30. |

## Features

- **Interactive Q&A**: Users can input questions to receive answers from the dataset.
- **Data Loading**: Efficiently loads and processes data from the CSV file.
  
## Usage

1. Open the notebook in Google Colab.
2. Set up your Google API key and configure the Chroma DB.
3. Run the cells sequentially to load the data and initialize the FAQ bot.
4. Input your questions in the designated field to receive answers.

## Requirements

- Google Colab environment
- Google API services (with API key)
- Chroma DB installed and configured
- Basic knowledge of Python and data manipulation
