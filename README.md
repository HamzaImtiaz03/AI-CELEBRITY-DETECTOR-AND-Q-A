# AI Celebrity Detector and Q/A System: Intelligent Image Analysis Platform

![AI Celebrity Detector Banner](https://github.com/HamzaImtiaz03/AI-CELEBRITY-DETECTOR-AND-Q-A/blob/main/Project%20Tech%20Stacks%20Image.png?raw=true) <!-- Replace with actual image URL or embed if available -->

[![GitHub Repo](https://img.shields.io/badge/GitHub-Repo-blue?logo=github)](https://github.com/HamzaImtiaz03/AI-Celebrity-Detector-QA) <!-- Update with actual repo URL -->
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10](https://img.shields.io/badge/Python-3.10-green?logo=python)](https://www.python.org/)
[![Docker](https://img.shields.io/badge/Docker-Enabled-blue?logo=docker)](https://www.docker.com/)
[![Kubernetes Deployed](https://img.shields.io/badge/Deployed-Kubernetes-orange?logo=kubernetes)](https://kubernetes.io/)
[![GCP Hosted](https://img.shields.io/badge/Hosted-GCP-brightgreen?logo=google-cloud)](https://cloud.google.com/)
[![CircleCI CI/CD](https://img.shields.io/badge/CI%2FCD-CircleCI-blue?logo=circleci)](https://circleci.com/)

## Overview

The **AI Celebrity Detector and Q/A System** is a cutting-edge AI application that identifies celebrities in uploaded images and provides insightful answers to user queries about them. Integrating advanced vision transformers for detection and Groq-powered natural language processing for Q/A, it offers a seamless, interactive experience via a Flask-based web interface with HTML/CSS styling.

This project showcases a complete MLOps pipeline, from local development to automated deployment on Google Kubernetes Engine (GKE). It leverages Docker for containerization, CircleCI for CI/CD workflows (including building/pushing images to Google Artifact Registry and deploying to GKE), and secure secret management for API keys. Ideal for entertainment apps, media analysis, or educational tools, it combines computer vision, NLP, and cloud-native practices for scalable, reliable performance.

## Key Features

- **Celebrity Detection**: Uses vision transformers and OpenCV to accurately detect and identify celebrities in images.
- **Interactive Q/A Engine**: Groq-integrated NLP for answering queries about detected celebrities, such as biographies, filmographies, or trivia.
- **Image Handling**: Robust upload and processing routes in Flask for handling user-submitted images.
- **Web Interface**: Responsive HTML/CSS frontend for image uploads, detection results, and Q/A interactions.
- **Secure Configurations**: Environment variables and Kubernetes secrets for managing API keys (e.g., GROQ_API_KEY).
- **Automated CI/CD**: CircleCI pipeline for code checkout, Docker image build/push to GAR, and deployment to GKE on every push.
- **Containerization & Orchestration**: Dockerized app with Kubernetes Deployment (1 replica) and LoadBalancer Service for scalability.
- **Cloud-Native Deployment**: Hosted on GKE with pre-configured GCP APIs, service accounts, and artifact registry.

## Architecture

The system follows a modular architecture spanning development, containerization, versioning/CI, and deployment, as illustrated below:

![Project Architecture Flowchart](https://github.com/HamzaImtiaz03/AI-CELEBRITY-DETECTOR-AND-Q-A/blob/main/100%20-%20Introduction%20to%20the%20Project%20-%20Celebrity+Detector+QA+Workflow.png?raw=true) <!-- Replace with actual image URL or embed -->

### High-Level Breakdown:
1. **Development & Setup**: Project initialization with API configs, image handling, celebrity detection logic, Q/A engine, routes, and Flask app.
2. **Containerization & Deployment**: Dockerfile for building images, Kubernetes YAML for deployments/services on GKE.
3. **Version Control & CI**: GitHub for versioning, CircleCI pipeline for automated builds, pushes to GAR, and GKE rollouts.
4. **Cloud Integration**: GCP setup with GKE clusters, Artifact Registry, service accounts, and API enablement.

This design ensures efficiency, security, and seamless updates from code to production.

## Technologies Used

- **Core Frameworks**: Flask (web app), OpenCV (image processing), NumPy (data handling), Requests (API calls).
- **AI/ML**: Groq (NLP/QA), Vision Transformers (celebrity detection).
- **Frontend**: HTML/CSS (responsive UI).
- **Environment Management**: Python-dotenv (secrets handling).
- **Containerization & Orchestration**: Docker (containerization), Kubernetes (GKE deployments), Kubectl (management).
- **CI/CD**: CircleCI (pipelines with GCP integration).
- **Cloud Platform**: Google Cloud Platform (GKE, Artifact Registry, Compute Engine, etc.).
- **Version Control**: GitHub.
- **Packaging**: Setuptools (via setup.py).

Full dependencies are listed in `requirements.txt`.

## Installation

### Prerequisites
- Python 3.10+
- Git
- Docker (for containerization)
- Google Cloud Platform Account (for deployment)
- API Keys: Groq (stored in `.env`)
- Optional: Kubectl, gcloud CLI for local GKE testing

### Steps
1. **Clone the Repository**:
   ```
   git clone https://github.com/HamzaImtiaz03/AI-Celebrity-Detector-QA.git <!-- Update with actual repo URL -->
   cd AI-Celebrity-Detector-QA
   ```

2. **Set Up Virtual Environment** (Recommended):
   ```
   python -m venv venv
   source venv/bin/activate  # On Unix/Mac
   # Or on Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**:
   ```
   pip install -e .
   ```

4. **Configure Environment Variables**:
   Create a `.env` file in the root directory:
   ```
   GROQ_API_KEY=your_groq_api_key
   # Add other variables as needed
   ```

## Usage

1. **Run the Application Locally**:
   ```
   python app.py
   ```
   - Access the app at `http://localhost:5000`.
   - Upload an image containing a celebrity, view detection results, and ask questions for AI-generated answers.

2. **Example Interactions**:
   - Upload a photo of a celebrity → System detects and displays identity.
   - Query: "What movies has this celebrity starred in?" → Receives detailed response via Groq.

3. **Customization**:
   - Extend detection models in celebrity detector code.
   - Add new routes or UI elements in Flask app.

## Deployment

This project includes an automated CI/CD pipeline for deployment to GKE via CircleCI.

### Prerequisites
- GCP Project with enabled APIs (Kubernetes Engine, Container Registry, etc.) as per `FULL_DOCUMENTATION.md`.
- GKE Cluster and Artifact Registry created.
- Service Account with roles (Storage Admin, Artifact Registry Admin, etc.) and JSON key.
- CircleCI account connected to GitHub.

### Pipeline Overview (via .circleci/config.yml)
1. **Checkout Code**: Pull from GitHub.
2. **Build Docker Image**: Authenticate GCP, build, and push to Artifact Registry.
3. **Deploy to GKE**: Configure cluster access, apply Kubernetes YAML, and restart deployment.

### Detailed Steps
- Follow `FULL_DOCUMENTATION.md` for GCP setup, service account creation, Base64 key encoding, CircleCI config, environment variables (GCLOUD_SERVICE_KEY, GOOGLE_PROJECT_ID, etc.), and Kubernetes secrets.
- Build and run Docker image locally:
  ```
  docker build -t celebrity-detector-qa .
  docker run -p 5000:5000 celebrity-detector-qa
  ```
- Deploy to GKE:
  ```
  gcloud container clusters get-credentials your-cluster --region your-region --project your-project
  kubectl create secret generic llmops-secrets --from-literal=GROQ_API_KEY=your_key
  kubectl apply -f kubernetes-deployment.yaml
  ```
- Trigger pipeline via GitHub push; CircleCI handles build/deploy automatically.
- Access the app via the LoadBalancer external IP on port 80.

## Contributing

Contributions are welcome to enhance detection accuracy, add features, or improve pipelines! To contribute:
1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/YourFeature`).
3. Commit changes (`git commit -m 'Add YourFeature'`).
4. Push to the branch (`git push origin feature/YourFeature`).
5. Open a Pull Request.

Follow best practices and include tests/documentation.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Frameworks: Flask, OpenCV, Groq, Vision Transformers.
- Tools: Docker, Kubernetes, CircleCI, GCP (GKE, Artifact Registry).
- Inspired by AI applications in image recognition and interactive Q/A for media and entertainment.

For questions or support, open an issue on GitHub or contact [Hamza Imtiaz](mailto:hamzaimtiaz8668@gmail.com).

---

*Built by Hamza Imtiaz | Unveiling Celebrities with AI Precision*