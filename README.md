# GCP-Cloud-Run
<img width="1424" height="752" alt="Gemini_Generated_Image_uvqsshuvqsshuvqs" src="https://github.com/user-attachments/assets/2716458b-a87e-40ca-8631-fd80d49ee02d" />


This is a clean, professional `README.md` structure designed to make your repository look high-quality and easy to navigate. It uses clear headings, code blocks with syntax highlighting, and a logical flow.

---

```markdown
# 🚀 Google Cloud Run: Hello World Deployment

A streamlined guide to containerizing a "Hello World" application and deploying it to **Google Cloud Run** using **Artifact Registry** and **Cloud Build**.

---

## 🛠️ Prerequisites

Before you begin, ensure you have the [Google Cloud CLI](https://cloud.google.com/sdk/docs/install) installed and initialized.

### 1. Enable APIs
Enable the necessary services for Cloud Run and Artifact Registry:
```bash
gcloud services enable \
    run.googleapis.com \
    artifactregistry.googleapis.com
```

### 2. Configure Environment
Set your preferred deployment region:
```bash
export LOCATION="us-west1"
gcloud config set compute/region $LOCATION
```

---

## 📦 Setup & Build

### 1. Create Project Directory
```bash
mkdir helloworld && cd helloworld
# Add your application source and Dockerfile here
```

### 2. Prepare Artifact Registry
Create a Docker repository to store your container images:
```bash
gcloud artifacts repositories create my-repository \
    --repository-format=docker \
    --location=$LOCATION \
    --description="Docker repository for Cloud Run images"
```

Configure Docker to authenticate with the registry:
```bash
gcloud auth configure-docker $LOCATION-docker.pkg.dev
```

### 3. Build the Image
Use **Cloud Build** to build and push your image to the registry automatically:
```bash
gcloud builds submit --tag $LOCATION-docker.pkg.dev/$GOOGLE_CLOUD_PROJECT/my-repository/helloworld
```

---

## 🧪 Local Testing

To verify the container is working correctly, run it locally (or in Cloud Shell):

```bash
# Run the container
docker run -d -p 8080:8080 $LOCATION-docker.pkg.dev/$GOOGLE_CLOUD_PROJECT/my-repository/helloworld

# Test the endpoint
curl http://localhost:8080
```
> **Expected Output:** `Hello World!`

---

## 🚀 Deployment

Deploy the image to **Cloud Run** with public access enabled:

```bash
gcloud run deploy helloworld \
    --image $LOCATION-docker.pkg.dev/$GOOGLE_CLOUD_PROJECT/my-repository/helloworld \
    --allow-unauthenticated \
    --region=$LOCATION
```

Once the deployment is complete, the CLI will provide a service URL where your application is live!

---

## 🧹 Cleanup (Optional)
To avoid incurring charges, you can delete the resources:
```bash
gcloud run services delete helloworld --region=$LOCATION
gcloud artifacts repositories delete my-repository --location=$LOCATION
```
```
