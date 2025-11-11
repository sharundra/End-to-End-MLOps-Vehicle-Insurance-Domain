# 🚀 End-to-End MLOps Project — Vehicle Insurance Risk Prediction

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python)
![MLOps](https://img.shields.io/badge/MLOps-End--to--End-brightgreen)
![AWS](https://img.shields.io/badge/Deployed%20On-AWS-orange?logo=amazonaws)
![MongoDB](https://img.shields.io/badge/Database-MongoDB-green?logo=mongodb)
![CI/CD](https://img.shields.io/badge/CI/CD-GitHub%20Actions-blue?logo=githubactions)

> **Goal:** Develop and deploy a complete Machine Learning pipeline in the **Vehicle Insurance domain**, covering **data ingestion → preprocessing → model training → evaluation → cloud deployment → CI/CD automation.**

---

## 📖 Overview

This project demonstrates a **production-grade MLOps workflow** — transforming raw vehicle insurance data into a fully automated, cloud-deployed prediction system.

It’s built to showcase:

* **Scalable ML architecture (modular `src/` design)**
* **Cloud database integration (MongoDB Atlas)**
* **Model versioning and storage on AWS S3**
* **Web app deployment on EC2 via Docker + GitHub Actions**
* **End-to-End CI/CD automation pipeline**

---

## 🧠 Tech Stack

| Layer                    | Tools & Technologies                                           |
| ------------------------ | -------------------------------------------------------------- |
| **Language**             | Python 3.11                                                    |
| **Data Storage**         | MongoDB Atlas                                                  |
| **ML Libraries**         | pandas, scikit-learn, numpy                                    |
| **Model Tracking**       | AWS S3 (model registry)                                        |
| **Web Framework**        | Flask, HTML/CSS                                                |
| **Containerization**     | Docker                                                         |
| **CI/CD**                | GitHub Actions                                                 |
| **Deployment**           | AWS EC2 (Ubuntu, self-hosted runner)                           |
| **Environment**          | Conda Virtual Environment                                      |
| **Logging & Exceptions** | Custom logger and handler under `src/logger` & `src/exception` |

---

## 🏗️ Project Architecture

```
End-to-End-MLOps-Vehicle-Insurance-Domain/
│
├── .github/workflows/aws.yaml         # CI/CD Pipeline Definition
├── src/                               # Modular source package
│   ├── components/                    # Core ML pipeline stages
│   ├── configuration/                 # DB & AWS configurations
│   ├── cloud_storage/                 # AWS S3 interactions
│   ├── entity/                        # Config & artifact entities
│   ├── exception/                     # Custom exception handler
│   ├── logger/                        # Logging setup
│   ├── pipeline/                      # Training & prediction pipelines
│   ├── utils/                         # Helper functions
│   └── constants/                     # Global constants
│
├── app.py                             # Flask web app entry point
├── Dockerfile                         # Container definition
├── requirements.txt                   # Dependencies
├── pyproject.toml                     # Package setup
├── setup.py                           # Editable install (`-e .`)
├── notebook/                          # EDA & data experiments
│   ├── mongodb_demo.ipynb
│   └── exp-notebook.ipynb
└── README.md
```

---

## ⚙️ 1. Environment Setup

```bash
# Clone the repo
git clone https://github.com/<your-username>/End-to-End-MLOps-Vehicle-Insurance-Domain.git
cd End-to-End-MLOps-Vehicle-Insurance-Domain

# Create & activate conda env
conda create -n insurance python=3.11 -y
conda activate insurance

# Install dependencies
pip install -r requirements.txt
```

To use your local `src` package:

```bash
# Editable install for local development
echo "-e ." >> requirements.txt
pip install -r requirements.txt
```

---

## 🧩 2. MongoDB Atlas Integration

The project uses **MongoDB Atlas** for storing raw vehicle insurance data.

**Steps:**

1. Create an organization and project in MongoDB Atlas.
2. Create a free shared cluster (AWS, 512MB).
3. Add IP access rule: `0.0.0.0/0` (allow global access).
4. Get your connection URI for Python (Driver → 4.7+).
5. Push data using the demo notebook:

   ```
   notebook/mongodb_demo.ipynb
   ```
6. Verify via *Clusters → Browse Collections* in Atlas UI.

---

## 🧮 3. Data Ingestion → Preprocessing → Model Training

The complete pipeline is built modularly inside the `src/` package:

* **Data Ingestion:** Fetches data from MongoDB and splits into train/test sets.
* **Data Validation:** Schema check and data consistency validation.
* **Data Transformation:** Encoding, scaling, and preprocessing.
* **Model Training:** Trains ML model and stores it as a serialized artifact.
* **Model Evaluation:** Compares with previously deployed model.
* **Model Pusher:** Pushes best model to AWS S3.

Each step produces an **artifact** stored under the `artifact/` folder for traceability.

---

## ☁️ 4. AWS S3 and Model Registry

* AWS S3 acts as a **model registry** for versioned model storage.
* AWS access is established through `boto3`, configured in:

  ```
  src/configuration/aws_connection.py
  src/cloud_storage/aws_storage.py
  ```

You can set your credentials temporarily (recommended):

```bash
export AWS_ACCESS_KEY_ID="your-key"
export AWS_SECRET_ACCESS_KEY="your-secret"
```

Bucket configuration is defined in:

```
src/constants/__init__.py
```

---

## 🤖 5. Flask Web Application

The web interface is served via `app.py` using **Flask**.

Features:

* Upload vehicle data → get model predictions
* Train the model directly via UI
* Lightweight frontend (`templates/vehicledata.html` + `static/css/style.css`)

Run locally:

```bash
python app.py
```

Access at [http://localhost:5000](http://localhost:5000)

---

## 🐳 6. Dockerization

The app and pipeline are fully containerized using Docker.

```bash
docker build -t vehicle-insurance-app .
docker run -p 5000:5000 vehicle-insurance-app
```

---

## ⚙️ 7. CI/CD Pipeline (GitHub Actions + AWS EC2 + ECR)

**Pipeline Flow:**

1. **CI:** GitHub Actions builds and tests the Docker image.
2. **CD:** The image is pushed to AWS ECR.
3. **Deployment:** A self-hosted EC2 runner pulls the latest image and redeploys the container.

**Setup summary:**

* AWS credentials stored as GitHub secrets.
* ECR repo stores images (`vehicleproj`).
* EC2 Ubuntu instance runs as a **self-hosted runner**.
* Port 5000 opened for web access.

---

## 🧱 8. Key Highlights

✅ **End-to-End MLOps Automation** — data to deployment
✅ **AWS Cloud-Native Architecture** — S3, EC2, ECR, IAM
✅ **CI/CD via GitHub Actions** — real DevOps integration
✅ **Reusable Modular Design** — production-quality codebase
✅ **Logging & Exception Handling** — enterprise-grade reliability
✅ **Editable Local Package Setup** (`-e .`) — scalable project packaging
✅ **Deployed Flask App + Model Registry** — complete delivery loop

---

## 📊 Results

* Fully automated pipeline for vehicle insurance claim risk modeling.
* Model retraining, versioning, and redeployment supported.
* Cloud-ready architecture with reproducibility and traceability.
* Zero manual steps post CI/CD trigger — **true continuous deployment**.

---

## 💡 Future Enhancements

* Integrate MLflow for experiment tracking.
* Deploy via Kubernetes on AWS EKS.
* Add monitoring via AWS CloudWatch.
* Extend pipeline to support multiple models and A/B testing.

---

## 🧑‍💻 Author

**Sharad [Your Full Name]**
Data Scientist
🔗 [LinkedIn](https://www.linkedin.com/in/sharad-mishra-/)
💻 [GitHub](https://github.com/sharundra)

---

## 🏁 Conclusion

This project is a **real-world, production-ready MLOps workflow** — from dataset ingestion to cloud deployment — showcasing a strong grasp of **machine learning engineering, cloud computing, and DevOps practices**.
---

