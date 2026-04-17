# Conversational AI Agent

A professional conversational AI chatbot with modern web UI built with FastAPI. Supports both rule-based responses and OpenAI API integration.

## Features

- 🎨 **Modern Web UI** - Beautiful, responsive chat interface
- 🌓 **Dark Mode** - Toggle between light and dark themes
- 💬 **Real-time Chat** - Smooth messaging experience with typing indicators
- 🤖 **Dual Mode** - Rule-based (no API key) or OpenAI-powered responses
- 💾 **Persistent History** - Messages saved in browser localStorage
- 📱 **Mobile Responsive** - Works perfectly on all devices
- 🚀 **FastAPI Backend** - High-performance REST API
- 🐳 **Docker Ready** - Easy containerization and deployment
- ☁️ **Render Optimized** - One-click deployment to Render

## Screenshots

### Light Mode
Modern, clean interface with intuitive design.

### Dark Mode
Easy on the eyes for late-night conversations.

## API Endpoints

### GET /
Web UI - Interactive chat interface

### POST /chat
Send a message and get a response.

**Request:**
```json
{
  "message": "Hello!"
}
```

**Response:**
```json
{
  "response": "Hello! How can I help you today?"
}
```

### GET /health
Service health status.

## Local Development

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Run Locally

**Without OpenAI (rule-based):**
```bash
uvicorn main:app --reload --port 8000
```

**With OpenAI:**
```bash
export OPENAI_API_KEY="your-api-key-here"
uvicorn main:app --reload --port 8000
```

### 3. Test the API

```bash
curl -X POST http://localhost:8000/chat \
  -H "Content-Type: application/json" \
  -d '{"message": "Hello!"}'
```

## Docker

### Build Image

```bash
docker build -t conversational-ai-agent .
```

### Run Container

**Without OpenAI:**
```bash
docker run -p 8000:8000 conversational-ai-agent
```

**With OpenAI:**
```bash
docker run -p 8000:8000 \
  -e OPENAI_API_KEY="your-api-key-here" \
  conversational-ai-agent
```

## Deploy to Render

### Method 1: Using render.yaml (Recommended)

1. **Create GitHub Repository**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
   git push -u origin main
   ```

2. **Deploy on Render**
   - Go to [Render Dashboard](https://dashboard.render.com/)
   - Click "New" → "Blueprint"
   - Connect your GitHub repository
   - Render will automatically detect `render.yaml`
   - Click "Apply"

3. **Add Environment Variables (Optional)**
   - In Render dashboard, go to your service
   - Navigate to "Environment" tab
   - Add `OPENAI_API_KEY` if using OpenAI
   - Service will auto-deploy

### Method 2: Manual Web Service

1. **Create GitHub Repository** (same as above)

2. **Create Web Service on Render**
   - Go to [Render Dashboard](https://dashboard.render.com/)
   - Click "New" → "Web Service"
   - Connect your GitHub repository
   - Configure:
     - **Name:** conversational-ai-agent
     - **Environment:** Docker
     - **Plan:** Free
     - **Health Check Path:** /health

3. **Add Environment Variables**
   - `PORT`: 10000 (auto-set by Render)
   - `OPENAI_API_KEY`: your-key (optional)
   - `OPENAI_MODEL`: gpt-3.5-turbo (optional)

4. **Deploy**
   - Click "Create Web Service"
   - Wait for deployment (2-5 minutes)

### Access Your API

Your API will be available at:
```
https://your-service-name.onrender.com
```

Test it:
```bash
curl -X POST https://your-service-name.onrender.com/chat \
  -H "Content-Type: application/json" \
  -d '{"message": "Hello!"}'
```

## Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| PORT | No | 8000 | Server port (Render sets to 10000) |
| OPENAI_API_KEY | No | - | OpenAI API key for GPT responses |
| OPENAI_MODEL | No | gpt-3.5-turbo | OpenAI model to use |

## Project Structure

```
.
├── main.py              # FastAPI application
├── agent.py             # Conversational agent logic
├── requirements.txt     # Python dependencies
├── Dockerfile          # Docker configuration
├── render.yaml         # Render deployment config
├── .gitignore          # Git ignore rules
└── README.md           # This file
```

## How It Works

1. **Rule-Based Mode** (default):
   - Uses pattern matching for common queries
   - No external API required
   - Works immediately

2. **OpenAI Mode** (optional):
   - Set `OPENAI_API_KEY` environment variable
   - Uses GPT-3.5-turbo or GPT-4
   - Maintains conversation context
   - Falls back to rule-based on errors

## Notes

- Free tier on Render may spin down after inactivity
- First request after spin-down takes 30-60 seconds
- OpenAI API usage incurs costs
- Rule-based mode is free and always available

## License

MIT
