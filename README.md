# Ollama Docker with Local AI Chat

A lightweight, containerized chat interface powered by Ollama and built with Vue 3. This project provides a self-contained local LLM chat platform designed for testing, prototyping, and social engineering demonstrations.

## 🎯 Overview

**Ollama_docker** combines:
- **Ollama**: A local, open-source LLM runtime
- **Vue 3 + TypeScript**: A modern, reactive web interface
- **Docker**: Complete containerization for easy deployment

This setup allows you to run a fully functional AI chat system entirely on your local machine without external API dependencies.

## ✨ Features

- 🤖 **Local LLM**: Run large language models completely offline with Ollama
- 💬 **Chat Interface**: Intuitive web-based chat UI built with Vue 3
- 🔒 **Privacy-First**: All data stays local; no external API calls
- 🐳 **Docker Ready**: Single-command deployment with docker-compose
- 🛡️ **Demo-Ready**: Designed for security testing and social engineering demonstrations

## 📋 Prerequisites

- **Docker** & **Docker Compose** (or Node.js 18+ for local development)
- **Ollama** installed locally or via container
- At least 4GB RAM available (more for larger models)

## 🚀 Quick Start

### Option 1: Using Docker Compose (Recommended)

```bash
# Clone the repository
git clone https://github.com/htl3r-2135/Ollama_docker.git
cd Ollama_docker

# Start both Ollama and the web app
docker-compose up --build

# Access the chat interface at http://localhost:5173
```

### Option 2: Local Development

```bash
# Install dependencies
cd testing_LLM
npm install

# Start the development server
npm run dev

# Open your browser to http://localhost:5173
```

### Option 3: Production Build

```bash
cd testing_LLM

# Build for production
npm run build

# Preview production build
npm run preview
```

## 📁 Project Structure

```
.
├── README.md                    # This file
├── docker-compose.yml           # Docker Compose configuration
├── Dockerfile                   # Container setup for the app
├── testing_LLM/                 # Vue 3 frontend application
│   ├── src/                     # Source code (components, views, logic)
│   ├── public/                  # Static assets
│   ├── package.json             # Node dependencies
│   ├── vite.config.ts           # Vite bundler config
│   ├── tsconfig.json            # TypeScript config
│   └── README.md                # Frontend-specific documentation
└── .gitignore                   # Git ignore rules
```

## 🔧 Technology Stack

| Technology | Purpose |
|-----------|---------|
| **Vue 3** | Progressive JavaScript framework for the UI |
| **TypeScript** | Type-safe JavaScript |
| **Vite** | Next-generation frontend build tool |
| **Ollama** | Local LLM runtime engine |
| **Docker** | Containerization & orchestration |

## 🛠️ Configuration

### Ollama Models

By default, Ollama can run any model from its [library](https://ollama.ai/library). Common models for chat:

```bash
# Inside the container
ollama pull llama2          # Meta's Llama 2
ollama pull mistral         # Mistral 7B
ollama pull neural-chat     # Intel's Neural Chat
ollama pull orca-mini       # Small, fast model
```

### Environment Variables

If using custom Ollama API endpoints, configure them in:
- `testing_LLM/src/` (check for API client configuration)

## 📖 Usage

1. **Start the application** (via Docker or local dev)
2. **Open your browser** to `http://localhost:5173`
3. **Type your message** in the chat box
4. **Press Send** to interact with the LLM

The chat interface communicates with the Ollama API backend running on `http://localhost:11434`.

## 🔌 API Integration

The Vue app communicates with Ollama via its REST API:

```
Ollama API Endpoint: http://localhost:11434/api/generate
```

Example request structure:
```json
{
  "model": "llama2",
  "prompt": "Your message here",
  "stream": true
}
```

## 🎓 Use Cases

- **Prototyping**: Test LLM chat interfaces locally
- **Testing**: Evaluate model responses before production
- **Social Engineering Demos**: Demonstrate AI-assisted social engineering concepts
- **Education**: Learn about LLMs and web development together

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| Port 5173 already in use | Change port in `vite.config.ts` or kill the process |
| Ollama connection refused | Ensure Ollama container is running: `docker ps` |
| Out of memory | Reduce model size or allocate more Docker memory |
| Node modules missing | Run `cd testing_LLM && npm install` |

## 📝 Development

### Run tests
```bash
cd testing_LLM
npm run test
```

### Type checking
```bash
cd testing_LLM
vue-tsc --noEmit
```

### Build and preview
```bash
cd testing_LLM
npm run build
npm run preview
```

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report issues
- Suggest improvements
- Submit pull requests

## 📄 License

This project is provided as-is for educational and testing purposes.

## ⚠️ Disclaimer

This tool is designed for legitimate security testing and educational demonstrations. Ensure you have proper authorization before conducting any social engineering tests or security assessments.

## 📞 Support

For issues, questions, or feedback:
- Open an [issue](https://github.com/htl3r-2135/Ollama_docker/issues)
- Check existing issues for solutions

---

**Happy chatting! 🚀**
