# Manimatic

Manimatic is an intelligent web application that generates mathematical animations from natural language descriptions. By combining the power of Google's Gemini AI with the Manim animation engine, users can create complex mathematical visualizations without writing code.


https://github.com/user-attachments/assets/f1fefca7-a04b-4e00-8895-2a3c36fcbddb


## Overview

- **Natural Language Interface**: Describe animations in plain English and watch them come to life
- **Persistent Chat History**: Maintain context across sessions for iterative refinement
- **Production-Ready Architecture**: Scalable, containerized deployment with job queue support

## Technology Stack

### Backend Services

- **Flask**: RESTful API and application server
- **Google Gemini API**: LLM-powered code generation and validation
- **Manim**: Mathematical animation rendering engine
- **MongoDB**: Document storage for chat histories and metadata
- **Cloudinary**: Cloud-based media storage and CDN
- **Celery + Redis**: Asynchronous task queue for animation processing

### Frontend Application

- **Next.js 14+**: React framework with server-side rendering
- **TailwindCSS**: Responsive utility-first styling
- **Shadcn UI**: Accessible component library

## System Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │   API Gateway   │    │   Task Queue    │
│   (Vercel)      │◄──►│   (Flask)       │◄──►│   (Redis/Celery)│
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                │                       │
                                ▼                       ▼
                       ┌─────────────────┐    ┌─────────────────┐
                       │   Media Storage │    │   Render Workers│
                       │   (Cloudinary)  │    │   (Docker)      │
                       └─────────────────┘    └─────────────────┘
```

## Request Processing Pipeline

1. User submits prompt via frontend
2. Backend authenticates request and validates rate limits
3. Prompt is screened for safety compliance
4. Gemini generates optimized Manim code
5. Render workers execute code asynchronously
6. Output is transcoded and uploaded to Cloudinary
7. Animation URL is returned to client
8. Chat context is persisted for future interactions

## Getting Started

### Requirements

- Python 3.10+
- Node.js 16+
- MongoDB 4.4+
- FFmpeg 4.2+
- Gemini API key (obtain from [Google AI Studio](https://aistudio.google.com))
- Cloudinary account

### Backend Installation

```bash
git clone https://github.com/0xAllan123/Manimatic.git
cd Manimatic/backend

python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

pip install -r requirements.txt

# Configure environment variables (see .env.example)
export FLASK_APP=app.py
export FLASK_ENV=production
export GEMINI_API_KEY=your_key_here
export MONGODB_URI=your_connection_string
export CLOUDINARY_URL=your_credentials

flask run
```

### Frontend Installation

```bash
cd ../frontend

npm install

# Create .env.local
echo "NEXT_PUBLIC_API_URL=http://localhost:5000" > .env.local

npm run dev
```

## Roadmap

- [ ] Enhanced content filtering and validation policies
- [ ] Tiered subscription management system
- [ ] Performance optimization for render times
- [ ] Administrative monitoring dashboard
- [ ] Animation template library and examples
- [ ] WebSocket support for real-time rendering feedback

## Security

This project implements baseline safety measures. For production environments, ensure:

- **Input Validation**: Comprehensive sanitization of user prompts
- **Code Execution Sandbox**: Isolated, resource-limited Manim execution environments
- **Rate Limiting**: Per-user and global quotas to prevent resource exhaustion
- **Audit Logging**: Complete trace of all code generation and execution

⚠️ **Warning**: Deploy additional security infrastructure before running in production, including secure secret management, network isolation, and comprehensive logging.

## Contributing

Contributions are welcome. Please open an issue or submit a pull request.

## License

[MIT License](LICENSE)

## Authors

- **Allan Howarth** - [GitHub](https://github.com/0xAllan123)
