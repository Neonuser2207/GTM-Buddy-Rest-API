# GTM-Buddy-Rest-API
This repository contains the code and resources for an end-to-end NLP pipeline and microservice that performs multi-label classification, entity extraction, and summarization on sales/marketing call snippets. The service is containerized using Docker and can be run locally or deployed to a cloud platform like Heroku.

Table of Contents
Project Overview

Repository Structure

Setup Instructions

Running the Service

API Endpoints

Deliverables

Future Improvements

License

Project Overview
The project involves the following tasks:

Data Preparation & Multi-Label Text Classification:

Generate a synthetic dataset of sales/marketing call snippets.

Preprocess the text and train a multi-label classification model.

Entity Extraction:

Extract domain-specific entities using a dictionary lookup and Named Entity Recognition (NER).

Containerized Inference Service:

Build a REST API using FastAPI to expose classification, entity extraction, and summarization functionalities.

Containerize the API using Docker for easy deployment.

Repository Structure
Copy
fresher-ai-assignment/
├── data/
│   ├── calls_dataset.csv                # Synthetic dataset of call snippets
│   ├── domain_knowledge.json            # Domain-specific dictionary
│   ├── cleaned_calls_dataset.csv        # Preprocessed dataset
│   ├── train_dataset.csv                # Training dataset
│   └── test_dataset.csv                 # Test dataset
├── models/
│   └── classification_model.pkl         # Trained multi-label classification model
├── src/
│   ├── main.py                          # FastAPI application
│   ├── data_preprocessing.py            # Script for data cleaning and preprocessing
│   ├── model_training.py                # Script for training the classification model
│   └── entity_extraction.py             # Script for entity extraction
├── Dockerfile                           # Dockerfile for containerizing the API
├── requirements.txt                     # Python dependencies
├── README.md                            # This file
└── technical_report.pdf                 # Detailed technical report
Setup Instructions
Prerequisites
Python 3.9: Install Python from python.org.

Docker: Install Docker from docker.com.

Git: Install Git from git-scm.com.

Installation
Clone the repository:

bash
Copy
git clone https://github.com/your-username/fresher-ai-assignment.git
cd fresher-ai-assignment
Install Python dependencies:

bash
Copy
pip install -r requirements.txt
Download the spaCy model:

bash
Copy
python -m spacy download en_core_web_sm
Running the Service
Option 1: Run Locally
Start the FastAPI application:

bash
Copy
uvicorn src.main:app --host 0.0.0.0 --port 80
The API will be accessible at http://localhost:80.

Option 2: Run with Docker
Build the Docker image:

bash
Copy
docker build -t fresher-ai-api .
Run the Docker container:

bash
Copy
docker run -d -p 80:80 fresher-ai-api
The API will be accessible at http://localhost:80.

Option 3: Deploy to Heroku
Install the Heroku CLI and log in:

bash
Copy
heroku login
Create a new Heroku app:

bash
Copy
heroku create fresher-ai-api
Push the Docker container to Heroku:

bash
Copy
heroku container:push web -a fresher-ai-api
heroku container:release web -a fresher-ai-api
The API will be accessible at https://fresher-ai-api.herokuapp.com.

API Endpoints
POST /predict
Description: Accepts a text snippet and returns predicted labels, extracted entities, and a summary.

Request Body:

json
Copy
{
  "text": "We love the analytics, but CompetitorX has a cheaper subscription."
}
Response:

json
Copy
{
  "predicted_labels": ["Positive", "Pricing Discussion", "Competition"],
  "extracted_entities": {
    "dictionary_lookup": {
      "competitors": ["CompetitorX"],
      "features": ["analytics"],
      "pricing_keywords": []
    },
    "ner_entities": {
      "organizations": [],
      "dates": [],
      "locations": []
    }
  },
  "summary": "This is a summary of the text snippet."
}
