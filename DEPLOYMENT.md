# Render Deployment Guide for TDS Project

## Prerequisites
- GitHub account
- Render account (sign up at https://render.com)
- Your environment variables ready (.env file contents)

## Step 1: Push Your Code to GitHub

1. **Initialize Git repository:**
   ```bash
   cd /Users/sathishkesavan/Downloads/tds-project-1-main
   git init
   git add .
   git commit -m "Initial commit: FastAPI app for TDS project"
   ```

2. **Create a new GitHub repository:**
   - Go to https://github.com/new
   - Name it: `tds-project-api` (or any name you prefer)
   - Make it **Private** (important for security since it contains sensitive code)
   - Don't initialize with README, .gitignore, or license
   - Click "Create repository"

3. **Push to GitHub:**
   ```bash
   git branch -M main
   git remote add origin https://github.com/sathish-k7/tds-project-api.git
   git push -u origin main
   ```

## Step 2: Deploy on Render

### Option A: Using Render Dashboard (Recommended)

1. **Go to Render Dashboard:**
   - Visit https://dashboard.render.com
   - Click "New +" → "Web Service"

2. **Connect GitHub Repository:**
   - Click "Connect account" if you haven't connected GitHub
   - Find and select your `tds-project-api` repository
   - Click "Connect"

3. **Configure Web Service:**
   ```
   Name: tds-project-api
   Region: Oregon (US West)
   Branch: main
   Runtime: Python 3
   Build Command: ./build.sh
   Start Command: uvicorn app.main:app --host 0.0.0.0 --port $PORT
   Instance Type: Free
   ```

4. **Add Environment Variables:**
   Click "Advanced" → "Add Environment Variable" and add:
   ```
   GITHUB_TOKEN=your_github_personal_access_token
   GITHUB_USERNAME=your_github_username
   OPENAI_API_KEY=your_openai_api_key
   USER_SECRET=your_secret_key
   OPENAI_BASE_URL=https://aipipe.org/openai/v1
   ```
   
   **Important:** Use your actual values from your `.env` file. Never commit these values to Git!

5. **Click "Create Web Service"**
   - Render will start building and deploying your app
   - Wait for deployment to complete (usually 2-5 minutes)

6. **Get Your API URL:**
   - Once deployed, you'll get a URL like: `https://tds-project-api.onrender.com`
   - Your API endpoint will be: `https://tds-project-api.onrender.com/api-endpoint`

### Option B: Using render.yaml (Blueprint)

1. **Deploy using Blueprint:**
   - Go to https://dashboard.render.com/select-repo?type=blueprint
   - Select your repository
   - Render will detect the `render.yaml` file
   - Add the environment variables manually
   - Click "Apply"

## Step 3: Test Your Deployed API

```bash
curl -X POST https://tds-project-api.onrender.com/api-endpoint \
-H "Content-Type: application/json" \
-d '{
  "email": "24f1000011@ds.study.iitm.ac.in",
  "secret": "tdsproject1_2025",
  "task": "test-deployment",
  "round": 1,
  "nonce": "deploy-test-001",
  "brief": "Create a simple weather app to test deployment",
  "checks": [
    "App works correctly",
    "GitHub integration functional"
  ],
  "evaluation_url": "https://webhook.site/4d3d4f09-7a12-4207-b10e-f59ffdc7592e",
  "attachments": []
}'
```

## Step 4: Monitor Your Deployment

1. **View Logs:**
   - Go to your service in Render Dashboard
   - Click "Logs" tab to see real-time logs

2. **Check Health:**
   - Render automatically monitors your service
   - You'll see "Live" status when healthy

## Important Notes

⚠️ **Free Tier Limitations:**
- Service spins down after 15 minutes of inactivity
- First request after spin-down may take 30-60 seconds
- 750 hours/month of runtime

⚠️ **Security:**
- Never commit `.env` file to Git
- Use Render's environment variables feature
- Keep your repository private

⚠️ **Troubleshooting:**
- If deployment fails, check the build logs
- Ensure all dependencies are in requirements.txt
- Verify Python version matches runtime.txt

## Useful Commands

**View service status:**
```bash
curl https://tds-project-api.onrender.com/docs
```

**Redeploy (after code changes):**
```bash
git add .
git commit -m "Update: description of changes"
git push
```
Render will automatically detect changes and redeploy.

## Alternative: Manual Deploy

If you prefer not to use GitHub, you can deploy using Render's Git repository:
1. Go to https://dashboard.render.com
2. Click "New +" → "Web Service"
3. Choose "Public Git repository"
4. Enter your repository URL
5. Follow the same configuration steps

## Support

- Render Documentation: https://render.com/docs
- Render Community: https://community.render.com
- Your API docs (after deployment): https://your-app.onrender.com/docs