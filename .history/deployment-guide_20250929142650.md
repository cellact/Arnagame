# Arnagame Snake Game - GCP Deployment Guide

This guide explains how to deploy your Snake Game to Google Cloud Platform using Docker and nginx.

## Project Structure

```
Arnagame/
├── index.html          # The Snake Game HTML file
├── Dockerfile          # Docker configuration for nginx
├── nginx.conf          # nginx server configuration
├── docker-compose.yml  # Local testing configuration
├── cloudbuild.yaml     # Google Cloud Build configuration
├── app.yaml           # Google App Engine configuration
└── deployment-guide.md # This guide
```

## Local Testing

### Prerequisites
- Docker installed on your machine
- Docker Compose installed

### Test Locally
1. Build and run the container:
   ```bash
   docker-compose up --build
   ```

2. Open your browser and go to: `http://localhost:8080`

3. To stop the container:
   ```bash
   docker-compose down
   ```

## GCP Deployment Options

You have three main deployment options on GCP:

### Option 1: Google Cloud Run (Recommended)

#### Prerequisites
- Google Cloud SDK installed
- A GCP project with billing enabled
- Container Registry API enabled
- Cloud Run API enabled

#### Manual Deployment Steps

1. **Set up your GCP project:**
   ```bash
   # Set your project ID
   export PROJECT_ID=your-project-id
   gcloud config set project $PROJECT_ID
   
   # Enable required APIs
   gcloud services enable cloudbuild.googleapis.com
   gcloud services enable run.googleapis.com
   gcloud services enable containerregistry.googleapis.com
   ```

2. **Build and push the Docker image:**
   ```bash
   # Build the image
   docker build -t gcr.io/$PROJECT_ID/arnagame-snake:latest .
   
   # Push to Container Registry
   docker push gcr.io/$PROJECT_ID/arnagame-snake:latest
   ```

3. **Deploy to Cloud Run:**
   ```bash
   gcloud run deploy arnagame-snake \
     --image gcr.io/$PROJECT_ID/arnagame-snake:latest \
     --region us-central1 \
     --platform managed \
     --allow-unauthenticated \
     --port 80 \
     --memory 256Mi \
     --cpu 1
   ```

#### Automatic Deployment with Cloud Build

1. **Connect your repository to Cloud Build:**
   - Go to Google Cloud Console > Cloud Build > Triggers
   - Click "Create Trigger"
   - Connect your GitHub/GitLab repository
   - Set the trigger to use `cloudbuild.yaml`

2. **The `cloudbuild.yaml` will automatically:**
   - Build your Docker image
   - Push it to Container Registry
   - Deploy to Cloud Run

### Option 2: Google App Engine

1. **Deploy to App Engine:**
   ```bash
   gcloud app deploy app.yaml
   ```

2. **Open your app:**
   ```bash
   gcloud app browse
   ```

### Option 3: Google Kubernetes Engine (GKE)

For more advanced scenarios, you can deploy to GKE:

1. **Create a GKE cluster:**
   ```bash
   gcloud container clusters create snake-game-cluster \
     --num-nodes=3 \
     --zone=us-central1-a
   ```

2. **Deploy your application:**
   ```bash
   kubectl create deployment snake-game --image=gcr.io/$PROJECT_ID/arnagame-snake:latest
   kubectl expose deployment snake-game --type=LoadBalancer --port=80
   ```

## Configuration Details

### Dockerfile
- Uses `nginx:alpine` for a lightweight container
- Copies your HTML file to nginx's web directory
- Uses custom nginx configuration for optimization

### nginx.conf Features
- Gzip compression enabled
- Security headers configured
- Static asset caching
- Health check endpoint at `/health`

### Performance Optimizations
- Gzip compression for faster loading
- Browser caching for static assets
- Lightweight Alpine Linux base image
- Minimal resource requirements

## Environment Variables

You can customize the deployment by setting these environment variables:

- `PROJECT_ID`: Your GCP project ID
- `REGION`: Deployment region (default: us-central1)
- `SERVICE_NAME`: Cloud Run service name (default: arnagame-snake)

## Monitoring and Logs

### View logs:
```bash
# Cloud Run logs
gcloud run logs tail --service=arnagame-snake

# App Engine logs
gcloud app logs tail
```

### Monitor performance:
- Use Google Cloud Console > Monitoring
- Set up uptime checks for your deployed URL

## Troubleshooting

### Common Issues:

1. **Build fails:**
   - Ensure Docker is running
   - Check that all files are in the correct directory

2. **Deployment fails:**
   - Verify APIs are enabled
   - Check IAM permissions
   - Ensure billing is enabled

3. **Service not accessible:**
   - Verify `--allow-unauthenticated` flag is set
   - Check firewall rules

### Health Check
Your application includes a health check endpoint at `/health` that returns "healthy" when the service is running properly.

## Cost Optimization

- Cloud Run: Pay only for requests (very cost-effective for low traffic)
- App Engine: Automatic scaling with flexible pricing
- Consider setting up budget alerts in GCP Console

## Security Considerations

- The nginx configuration includes security headers
- HTTPS is automatically provided by GCP services
- Consider adding custom domain and SSL certificate for production use

## Next Steps

1. Set up a custom domain
2. Configure HTTPS with your own SSL certificate
3. Set up monitoring and alerting
4. Consider adding a CI/CD pipeline for automatic deployments
