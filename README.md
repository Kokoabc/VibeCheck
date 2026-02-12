Project Title: Multi-Emotion Predictive API
A high-performance FastAPI and Docker-based service for real-time emotional intelligence analysis.

###  Project Overview
This project provides a REST API that analyzes text and classifies it across 11 different emotional dimensions (Joy, Anger, Fear, etc.). It uses SVM (Support Vector Machines) models trained on specialized NLP datasets, containerized with Docker for seamless deployment.

###  Tech Stack
Language: Python 3.12.7

Framework: FastAPI (Uvicorn)

Machine Learning: Scikit-Learn, Joblib

NLP: SpaCy (en_core_web_sm)

DevOps: Docker

###  Key Features & Challenges Solved
Multi-Model Architecture: Unlike basic sentiment tools, this API runs 11 separate binary classifiers in parallel to provide a nuanced emotional profile.

Containerization: Fully Dockerized to solve the "it works on my machine" problem, ensuring the NLP environment and spaCy dependencies are consistent across any server.

Robust Error Handling: Implemented a "safety-first" loading system that allows the API to remain functional even if specific model files are missing or corrupted.

Input Validation: Uses Pydantic schemas to ensure incoming JSON data is structured correctly before processing.

###  Installation & Usage
Bash
# Clone the repository
git clone https://github.com/your-username/predictive-security-api

# Build the Docker image
docker build -t emotion-api .

# Run the container
docker run -p 8000:8000 emotion-api
Access the interactive API documentation at http://localhost:8000/docs

###  Lessons Learned 
Path Management: Navigated the transition from Windows-specific file paths (C:\Users\...) to Linux-based container paths to ensure cloud portability.

Model Persistence: Debugged AttributeError issues related to model serialization and versioning between training and production environments.

Efficiency: Optimized the pipeline to run the Tfidf Vectorizer once across all 11 models, reducing latency per request.# VibeCheck
