# FM / TPC / VL - FIFA World Cup 2026 Dashboard

Live dashboard for the FM office World Cup pool.

## Local development

```bash
docker build -t fm-worldcup .
docker run -p 8080:8080 fm-worldcup
# Open http://localhost:8080
```

## Deploy to Google Cloud Run

### One-time setup
```bash
# Install gcloud CLI if you haven't: https://cloud.google.com/sdk/docs/install
gcloud auth login
gcloud config set project YOUR_PROJECT_ID
```

### Deploy
```bash
# Build and push to Google Container Registry
gcloud builds submit --tag gcr.io/YOUR_PROJECT_ID/fm-worldcup

# Deploy to Cloud Run
gcloud run deploy fm-worldcup \
  --image gcr.io/YOUR_PROJECT_ID/fm-worldcup \
  --platform managed \
  --region us-central1 \
  --allow-unauthenticated \
  --port 8080
```

Cloud Run will give you a URL like:
`https://fm-worldcup-xxxxxxxx-uc.a.run.app`

Open that on any TV browser.

### Update the dashboard
Edit `index.html`, then re-run the deploy commands above.

## Auto-deploy via GitHub Actions (optional)

Push to main branch → automatically rebuilds and redeploys.
See `.github/workflows/deploy.yml` if you add that later.
