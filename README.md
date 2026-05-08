# LLM Chat Application

A full-stack Large Language Model (LLM) chat application built with modern web technologies and containerized services. This project features a Python FastAPI backend with vector database support, a React TypeScript frontend with real-time chat capabilities, and GPU-enabled inference services.

## 📋 Project Overview

This is a production-ready LLM chatbot application with the following architecture:

- **Backend**: Python FastAPI server handling chat APIs and business logic
- **Frontend**: Modern React + TypeScript UI with Tailwind CSS and Vite
- **Inference**: GPU-enabled vLLM server for LLM inference
- **Database**: PostgreSQL for persistent data storage
- **Vector DB**: Qdrant for semantic search and RAG (Retrieval-Augmented Generation)

## 🏗️ Project Structure

```
llm-model/
├── backend/                    # Python FastAPI backend
│   ├── Dockerfile             # Backend container configuration
│   ├── requirements.txt        # Python dependencies
│   ├── .env                    # Environment variables
│   └── app/
│       ├── main.py            # FastAPI main application
│       ├── models.py          # Data models and schemas
│       └── api/
│           └── chat.py        # Chat endpoint handlers
│
├── frontend/                   # React TypeScript frontend
│   ├── Dockerfile             # Frontend container with nginx
│   ├── package.json           # Node.js dependencies
│   ├── vite.config.ts         # Vite bundler configuration
│   ├── tailwind.config.js     # Tailwind CSS configuration
│   ├── tsconfig.json          # TypeScript configuration
│   └── src/
│       ├── App.tsx            # Main React component
│       ├── index.tsx          # React entry point
│       ├── index.css          # Global styles
│       └── components/
│           ├── ChatBox.tsx    # Main chat container
│           ├── ChatHeader.tsx # Header component
│           ├── ChatInput.tsx  # Message input component
│           └── MessageBubble.tsx # Message display component
│
├── inference/                  # LLM inference service
│   └── Dockerfile             # vLLM inference container
│
├── postgres/                   # PostgreSQL database
│   └── Dockerfile             # PostgreSQL container (uses official image)
│
├── qdrant/                     # Vector database
│   └── Dockerfile             # Qdrant container (uses official image)
│
└── .devcontainer/
    ├── devcontainer.json      # VS Code dev container config
    ├── docker-compose.yml     # Multi-container orchestration
    └── settings.json          # VS Code settings
```

## 🛠️ Tech Stack

### Backend
- **Framework**: FastAPI (Python 3.12)
- **Server**: Uvicorn with uvloop
- **Database**: PostgreSQL 15
- **Vector DB**: Qdrant

### Frontend
- **Library**: React 18+ with TypeScript
- **Bundler**: Vite
- **Styling**: Tailwind CSS + PostCSS
- **Server**: Nginx (production)

### Infrastructure
- **Container**: Docker & Docker Compose
- **Inference**: vLLM (Meta Llama 3.1 8B)
- **GPU Support**: NVIDIA CUDA 12.4.1

## 🚀 Getting Started

### Prerequisites
- Docker & Docker Compose installed
- VS Code with Dev Containers extension (optional but recommended)

### Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd NewRepo
   ```

2. **Open in Dev Container** (optional but recommended)
   - Opens VS Code with proper environment
   - All dependencies pre-configured
   - Dev container settings in `.devcontainer/devcontainer.json`

3. **Start all services**
   ```bash
   cd llm-model/.devcontainer
   docker-compose up -d
   ```

4. **Access the application**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:8000
   - Inference API: http://localhost:8001
   - PostgreSQL: localhost:5432

## 📦 Services

### Backend Service
- **Port**: 8000 (mapped to 80 inside container)
- **Runs**: FastAPI with Uvicorn
- **Features**:
  - Chat API endpoints
  - Data models and business logic
  - PostgreSQL integration
  - Vector database queries

### Frontend Service
- **Port**: 3000 (mapped to 80 inside container)
- **Runs**: Vite dev server (development) / Nginx (production)
- **Components**:
  - Chat interface with message display
  - Real-time chat input
  - Responsive design with Tailwind CSS
  - TypeScript type safety

### Inference Service
- **Port**: 8001 (mapped to 8000 inside container)
- **Runs**: vLLM OpenAI-compatible API
- **Model**: Meta-Llama-3.1-8B-Instruct
- **CPU**: Tested on Codespaces (works without GPU)
- **Can be**: Switched to GPU runtime if available

### PostgreSQL Database
- **Port**: 5432
- **Default User**: postgres
- **Default Password**: postgres
- **Default Database**: llm
- **Status**: Configured but commented out in docker-compose.yml

### Qdrant Vector Database
- **Port**: 6333
- **Purpose**: Semantic search and RAG support
- **Status**: Optional service (commented out in docker-compose.yml)

## 🔧 Development

### Local Development (Backend)
```bash
cd backend
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
export PYTHONPATH=/app/app
uvicorn app.main:app --reload
```

### Local Development (Frontend)
```bash
cd frontend
npm install
npm run dev
```

### Build Production
```bash
# Build frontend
cd frontend
npm run build

# Build all containers
cd .devcontainer
docker-compose build
```

## 🐳 Docker Commands

```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down

# Rebuild containers
docker-compose build --no-cache

# Run specific service
docker-compose up backend frontend
```

## 📝 Environment Variables

Create `.env` file in `llm-model/` or `llm-model/backend/`:

```env
# Backend
PYTHONPATH=/app/app
LOG_LEVEL=info

# Database
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_DB=llm
DATABASE_URL=postgresql://postgres:postgres@postgres:5432/llm

# Inference
INFERENCE_API_URL=http://inference:8000
```

## 🔌 API Endpoints

### Chat API
- `POST /chat/send` - Send a message
- `GET /chat/history` - Get chat history
- `DELETE /chat/clear` - Clear chat history

*See [backend/app/api/chat.py](llm-model/backend/app/api/chat.py) for detailed endpoints*

## 🚨 Known Issues & Notes

1. **Empty Dockerfiles**: `postgres/Dockerfile` and `qdrant/Dockerfile` are placeholders
   - These services use official Docker images
   - Custom Dockerfiles can be created if needed

2. **GPU Support**: 
   - Currently configured for CPU inference in Codespaces
   - Uncomment GPU runtime in docker-compose.yml if GPU is available

3. **Services Status**:
   - PostgreSQL and Qdrant are commented out in docker-compose.yml
   - Uncomment in `.devcontainer/docker-compose.yml` to enable them

## 📚 Resources

- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [React Documentation](https://react.dev/)
- [vLLM Documentation](https://docs.vllm.ai/)
- [Qdrant Documentation](https://qdrant.tech/documentation/)
- [Docker Documentation](https://docs.docker.com/)

## 👨‍💻 Contributing

1. Create a feature branch
2. Make your changes
3. Test locally with docker-compose
4. Create a pull request

## 📄 License

[Add your license here]

## 🤝 Support

For issues or questions, please open an GitHub issue or contact the development team. 
