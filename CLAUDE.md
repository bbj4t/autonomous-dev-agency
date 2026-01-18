# CLAUDE.md - Global Rules for Claude Code

This file contains global instructions and context for Claude Code when working on this project.

## Project Overview

This is an **Autonomous Multi-Agent Software Development Agency** - a self-hosted AI-native development framework optimized for voice-first interaction and local LLM inference.

### Infrastructure

| Server | IP | Role |
|--------|-----|------|
| AI Server (`ai`) | 192.168.86.56 | LLM inference, STT/TTS, databases |
| Windows Workstation | 192.168.86.38 | Development, fast GPU inference (RX 550) |
| East Server (`linux-home`) | 192.168.86.51 | Redis, monitoring, n8n |

### Key Technologies

- **LLM**: Ollama (CPU) on AI server, llama.cpp (Vulkan GPU) on Windows
- **STT**: Faster-Whisper
- **TTS**: Kokoro-82M
- **Databases**: PostgreSQL (state), ChromaDB (vectors)
- **Orchestration**: Docker Compose
- **Development**: Google Antigravity IDE, Trae.ai IDE

## Coding Standards

### Python

- Use Python 3.12+ features
- Type hints on all function signatures
- Async/await for I/O operations
- Pydantic for data validation
- Follow PEP 8 style guidelines

### Documentation

- Docstrings on all public functions
- README.md in each major directory
- Update CHANGELOG.md for significant changes

### Git

- Conventional commits: `feat:`, `fix:`, `docs:`, `refactor:`, `test:`
- Feature branches from `main`
- PR required for merge to `main`

## Project Structure

```
autonomous-dev-agency/
├── deploy/                 # Docker Compose and deployment scripts
├── voice-assistant/        # Gradio-based voice UI
├── mcp-servers/           # MCP servers for IDE integration
├── agents/                # Agent definitions and orchestration
├── PRPs/                  # Product Requirements Prompts
├── memory/                # Agent memory stores
├── docs/                  # Documentation
└── scripts/               # Utility scripts
```

## Commands Available

When using Claude Code, these custom commands are available in `.claude/commands/`:

- `/generate-prp` - Create a new Product Requirements Prompt
- `/execute-prp` - Implement from an existing PRP
- `/review-and-evolve` - Code review with system improvement
- `/security-audit` - Run security analysis

## Environment Variables

Required environment variables are documented in `.env.example`. Key ones:

- `OLLAMA_HOST` - Ollama API endpoint
- `POSTGRES_PASSWORD` - Database password
- `STT_URL` / `TTS_URL` - Voice pipeline endpoints

## Testing

- Run tests: `pytest tests/`
- Coverage target: 80%+
- Integration tests require Docker services running

## Deployment

1. AI Server: `cd deploy && docker compose up -d`
2. East Server: `cd deploy && docker compose -f docker-compose.east.yml up -d`
3. Health check: `./scripts/health-check.sh`

## Security Notes

- Never commit `.env` files
- Use secrets management for production
- All inter-service communication should use internal Docker network
- External access through Tailscale VPN only

## Performance Constraints

- AI Server: 32GB RAM, 6C/12T Xeon (CPU-only inference)
- Windows: 16GB RAM, RX 550 4GB (small models only via Vulkan)
- Target voice response latency: <3s for simple queries

## Contact

- Project Owner: Jim
- Primary focus: Voice-first AI development workflows
