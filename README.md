## Cloud Run CI/CD

```bash
gcloud builds submit --tag gcr.io/dcdingprject/hello-bang .

gcloud run deploy hw-cloudrun --image gcr.io/dcdingprject/hello-bang:latest --region  asia-southeast2 --allow-unauthenticated

gcloud run services replace service.yaml

gcloud iam service-accounts add-iam-policy-binding \
  279495356623-compute@developer.gserviceaccount.com \
  --member="serviceAccount:279495356623@cloudbuild.gserviceaccount.com" \
  --role="roles/iam.serviceAccountUser"
```

## Prepare to CI/CD

```yaml
steps:
  # Build the container image
  - name: "gcr.io/cloud-builders/docker"
    args: ["build", "-t", "gcr.io/PROJECT_ID/IMAGE", "."]
  # Push the container image to Container Registry
  - name: "gcr.io/cloud-builders/docker"
    args: ["push", "gcr.io/PROJECT_ID/IMAGE"]
  # Deploy container image to Cloud Run
  - name: "gcr.io/google.com/cloudsdktool/cloud-sdk"
    entrypoint: gcloud
    args:
      ["run", "deploy", "SERVICE-NAME", "--image", "gcr.io/PROJECT_ID/IMAGE", "--region", "REGION"]
images:
  - gcr.io/PROJECT_ID/IMAGE
```
