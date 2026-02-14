### Project Title: Multi-Emotion Predictive API
A high-performance FastAPI and Docker-based service for real-time emotional intelligence analysis.

###  Project Overview
This project provides a REST API that analyzes text and classifies it across 11 different emotional dimensions (Joy, Anger, Fear, etc.). It uses SVM (Support Vector Machines), Linear regression, and KNN (K-nearest neighbour) models trained on specialized NLP datasets, containerized with Docker for seamless deployment.

##  Table of Contents
* [Project Overview](#-project-overview)
* [Tech Stack](#️-tech-stack)
* [Technical Challenges & Solutions](#-technical-challenges--solutions)
* [Installation & Usage](#-installation--usage)
* [API Documentation](#-api-documentation)
* [Future Roadmap](#-future-roadmap)
* [About the Author](#-about-the-author)


  

<img width="1836" height="881" alt="api_documentation" src="https://github.com/user-attachments/assets/fae3b8d2-a1cb-4d97-a22b-0bd2c89ec7cc" />
<img width="849" height="228" alt="uvicorn_running_message" src="https://github.com/user-attachments/assets/71a4efc5-8f42-45bb-bf09-0b4edef09454" />


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
https://github.com/Kokoabc/VibeCheck.git

# Build the Docker image
docker build -t emotion-api .

# Run the container
docker run -p 8000:8000 emotion-api
Access the interactive API documentation at http://localhost:8000/docs

###  Lessons Learned 
Path Management: Navigated the transition from Windows-specific file paths (C:\Users\...) to Linux-based container paths to ensure cloud portability.

Model Persistence: Debugged AttributeError issues related to model serialization and versioning between training and production environments.

Efficiency: Optimized the pipeline to run the Tfidf Vectorizer once across all 11 models, reducing latency per request.


###  Technical Challenges & Solutions
1. Cross-Platform Path Compatibility (Windows vs. Linux)
The Challenge: Initially, the application used hardcoded Windows absolute paths (e.g., C:\Users\...\models). When moved into a Docker container (which runs on Linux), the application crashed because it couldn't find the C: drive.

The Solution: I refactored the file-loading logic to use relative paths and the os library. This ensured that the API could locate the models regardless of the operating system or hosting environment.

2. Robust Model Loading (The "Missing Model" Problem)
The Challenge: Loading 11 separate SVM, Linear regression, and KNN models meant that if a single .joblib file was missing or corrupted, the entire API would fail to start.

The Solution: I implemented a dynamic loading loop with safety checks. The system now scans the trained_models directory on startup, logs which emotions are available, and gracefully skips any missing files. This allows the service to maintain high availability even during partial data updates.

3. Environment Standardization with Docker
The Challenge: Faced "Inconsistent Version" warnings and library mismatches (scikit-learn and spaCy) between the development laptop and the production environment.

The Solution: I engineered a Dockerfile that standardizes the Python runtime and dependencies. By containerizing the app, I eliminated the "it works on my machine" variable, ensuring the TfidfVectorizer and SVM, Linear regression, and KNN models behave identically in testing and deployment.


###  Future Roadmap
While the core API is functional, I have planned the following enhancements to scale the project into a production-grade security tool:

 Model Optimization & Quantization: Currently, the API loads 11 separate SVM, Linear regression, and KNN models. I plan to explore Multi-label Learning to condense these into a single model, reducing the memory footprint and improving inference speed.

 Frontend Dashboard: Developing a React or Streamlit dashboard to visualize emotional trends over time, allowing security analysts to see "emotional spikes" in data streams.

 Authentication & Rate Limiting: Implementing JWT (JSON Web Tokens) and API key management to secure the endpoints and prevent unauthorized usage.

 CI/CD Pipeline: Setting up GitHub Actions to automatically build and test the Docker image every time code is pushed, ensuring the API never breaks during updates.

 Cloud Deployment: Moving the containerized service from local Docker to AWS ECS or Google Cloud Run for global scalability.


 ## 👤 About the Author

**Mopelola Opeifa** *Aspiring AI & Security Engineer*

I am a developer passionate about the intersection of **Machine Learning** and **Cybersecurity**. This project was born out of a desire to understand how to deploy complex ML models into scalable, production-ready environments using Docker and FastAPI.

* https://www.credly.com/badges/4b46121e-5f1f-4d7f-8e76-55f369d38e29/public_url
* **LinkedIn:** www.linkedin.com/in/mopelola-opeifa-3751a0344
* **Interests:** Cloud infrastructure, NLP, Predictive Analytics.
