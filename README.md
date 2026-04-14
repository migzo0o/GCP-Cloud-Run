# GCP-Cloud-Run
<img width="1424" height="752" alt="Gemini_Generated_Image_uvqsshuvqsshuvqs" src="https://github.com/user-attachments/assets/2716458b-a87e-40ca-8631-fd80d49ee02d" />


Enable Cloud Run API
gcloud services enable run.googleapis.com artifactregistry.googleapis.com

Set Location
gcloud config set compute/region <REGION>

You can add it as a bash variable 
export LOCATION="us-west1"

Add these files to a folder called helloworld

mkdir helloworld && cd helloworld

* Create a new Docker repository named my-repository
  gcloud artifacts repositories create my-repository \
    --repository-format=docker \
    --location=$LOCATION \
    --description="Docker repository"

* Configure Docker to authenticate requests for Artifact Registry
  gcloud auth configure-docker $LOCATION-docker.pkg.dev

* Build your container image using Cloud Build
  gcloud builds submit --tag $LOCATION-docker.pkg.dev/$GOOGLE_CLOUD_PROJECT/my-repository/helloworld

- To run and test the application locally from Cloud Shell
  docker run -d -p 8080:8080 $LOCATION-docker.pkg.dev/$GOOGLE_CLOUD_PROJECT/my-repository/helloworld

  then curl http://localhost:8080
  it should print Hello World!

* Deploy your containerized application to Cloud Run
  gcloud run deploy helloworld \
    --image $LOCATION-docker.pkg.dev/$GOOGLE_CLOUD_PROJECT/my-repository/helloworld \
    --allow-unauthenticated \
    --region=$LOCATION

  
  
