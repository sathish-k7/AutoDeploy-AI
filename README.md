# TDS Project 1 - Automated App Generator API

A FastAPI application that automatically generates web applications based on user requirements, creates GitHub repositories, and deploys them to GitHub Pages.

## Features

- 🤖 AI-powered code generation using OpenAI
- 🔄 GitHub repository creation and management
- 📄 Automatic GitHub Pages deployment
- 🔔 Webhook notifications on completion
- 🔐 Secure authentication with secrets
- 📦 Support for file attachments
- ♻️ Duplicate request detection

## Local Development

### Prerequisites

- Python 3.13.7
- GitHub account and token
- OpenAI API key

### Setup

1. **Create a virtual environment:**
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure environment variables:**
   Create a `.env` file with:
   ```env
   GITHUB_TOKEN=your_github_token
   GITHUB_USERNAME=your_github_username
   OPENAI_API_KEY=your_openai_api_key
   USER_SECRET=your_secret_key
   OPENAI_BASE_URL=https://aipipe.org/openai/v1
   ```

4. **Run the application:**
   ```bash
   uvicorn app.main:app --reload
   ```

The API will be available at `http://127.0.0.1:8000`

## API Documentation

Once running, visit:
- Interactive API docs: `http://127.0.0.1:8000/docs`
- Alternative docs: `http://127.0.0.1:8000/redoc`

## API Endpoint

### POST `/api-endpoint`

Generate and deploy a web application.

**Request Body:**
```json
{
  "email": "user@example.com",
  "secret": "your_secret",
  "task": "project-name",
  "round": 1,
  "nonce": "unique-identifier",
  "brief": "Description of the app to generate",
  "checks": ["Requirement 1", "Requirement 2"],
  "evaluation_url": "https://webhook.site/your-id",
  "attachments": []
}
```

**Example:**
```bash
curl -X POST http://127.0.0.1:8000/api-endpoint \
-H "Content-Type: application/json" \
-d '{
  "email": "test@example.com",
  "secret": "tdsproject1_2025",
  "task": "weather-app",
  "round": 1,
  "nonce": "test-001",
  "brief": "Create a weather app with city search",
  "checks": ["Has README", "Works on mobile"],
  "evaluation_url": "https://webhook.site/your-id",
  "attachments": []
}'
```

## Deployment

See [DEPLOYMENT.md](DEPLOYMENT.md) for detailed instructions on deploying to Render.

### Quick Deploy to Render

1. Push code to GitHub
2. Connect repository to Render
3. Add environment variables
4. Deploy!

Your API will be available at `https://your-app.onrender.com`

## Project Structure

```
tds-project-1-main/
├── app/
│   ├── __init__.py
│   ├── main.py              # FastAPI application
│   ├── llm_generator.py     # OpenAI integration
│   ├── github_utils.py      # GitHub API functions
│   ├── notify.py            # Webhook notifications
│   └── signature.py         # Request signing
├── .env                     # Environment variables (not in git)
├── .gitignore              # Git ignore rules
├── requirements.txt        # Python dependencies
├── runtime.txt            # Python version
├── Procfile               # Process file for deployment
├── build.sh               # Build script for Render
├── render.yaml            # Render configuration
└── README.md              # This file
```

## How It Works

1. Receives a request with project requirements
2. Uses OpenAI to generate code based on the brief
3. Creates a GitHub repository
4. Commits generated files (HTML, README, LICENSE)
5. Enables GitHub Pages
6. Sends completion notification to evaluation URL

## Development

### Running Tests

```bash
python test_github.py
```

### Checking Logs

The application logs to stdout. In production, check Render logs.

## Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `GITHUB_TOKEN` | GitHub personal access token | Yes |
| `GITHUB_USERNAME` | Your GitHub username | Yes |
| `OPENAI_API_KEY` | OpenAI API key | Yes |
| `USER_SECRET` | Secret for request authentication | Yes |
| `OPENAI_BASE_URL` | OpenAI API base URL | No |

## License

MIT License - See LICENSE file for details

## Support

For issues or questions:
- Check the [DEPLOYMENT.md](DEPLOYMENT.md) guide
- Review API documentation at `/docs`
- Check application logs


