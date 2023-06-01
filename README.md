## Cloud Run CI/CD

```javascript
gcloud builds submit --tag gcr.io/dcdingprject/hello-bang .

gcloud run deploy hw-cloudrun --image gcr.io/dcdingprject/hello-bang:latest --region  asia-southeast2 --allow-unauthenticated

// gcloud run services replace service.yaml
```
