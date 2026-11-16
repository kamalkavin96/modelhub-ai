# ModelHub AI

**One Platform. Multiple AI Providers. Unified AI Access.**

ModelHub AI is an extensible AI model management platform designed to simplify working with multiple Large Language Model (LLM) providers through a unified interface.

It provides centralized provider configuration, API key management, model discovery, free and paid model catalogues, and a unified AI interface accessible through a Python SDK or REST API.

## Key Features

- **Multi-Provider Support:** Integrate Groq, NVIDIA, OpenRouter, Google Gemini, Cerebras, Together AI, and other AI providers.
- **API Key Management:** Securely store, encrypt, validate, and manage multiple API keys per provider.
- **Model Discovery:** Automatically discover and synchronize available models.
- **Free & Paid Models:** Maintain model availability, pricing, and access-tier information.
- **Unified AI Interface:** Interact with different providers through a consistent API.
- **Python SDK:** Integrate AI capabilities into Python applications.
- **REST API Gateway:** Expose AI functionality to Java, Python, JavaScript, and other applications.
- **SQLite Database:** Automatically initialize and manage a local database.
- **Provider Fallback:** Configure alternative providers when a model or provider becomes unavailable.
- **Usage Analytics:** Monitor requests, token consumption, and estimated costs.

## Architecture

```text
                  MODELHUB AI
                       |
          +------------+------------+
          |                         |
      Python SDK                 REST API
          |                         |
          +------------+------------+
                       |
                  Core Engine
                       |
          +------------+------------+
          |            |            |
       Provider      Model        API Key
       Manager      Registry      Manager
          |            |            |
          +------------+------------+
                       |
                   AI Gateway
                       |
        +--------------+--------------+
        |              |              |
       Groq          NVIDIA       OpenRouter
        |              |              |
        +--------------+--------------+
                       |
                   AI Response
```

## Supported Providers

Planned integrations:

- Groq
- NVIDIA NIM
- OpenRouter
- Google Gemini
- Cerebras
- Together AI
- Fireworks AI
- Mistral AI
- DeepSeek
- Hugging Face
- OpenAI

The architecture supports adding custom providers through an extensible provider adapter interface.

## Technology Stack

| Component | Technology |
|---|---|
| Core Engine | Python |
| Backend | FastAPI |
| Database | SQLite |
| ORM | SQLAlchemy |
| Validation | Pydantic |
| HTTP Client | HTTPX |
| Encryption | Cryptography |
| Frontend | React + Material UI |
| SDK Packaging | Python |

## Integration

ModelHub AI is designed to support two integration modes.

### 1. Local SDK

Install and initialize ModelHub directly inside a Python application.

```bash
pip install modelhub-ai
```

```python
from modelhub import ModelHub

hub = ModelHub(
    api_key="your-modelhub-api-key"
)

response = hub.chat.completions.create(
    model="groq/your-model-id",
    messages=[
        {
            "role": "user",
            "content": "Explain microservices"
        }
    ]
)

print(response.content)
```

### 2. REST API

Run ModelHub as a centralized AI gateway and access it from any application.

```python
from openai import OpenAI

client = OpenAI(
    base_url="http://localhost:8000/v1",
    api_key="your-modelhub-api-key"
)

response = client.chat.completions.create(
    model="groq/your-model-id",
    messages=[
        {
            "role": "user",
            "content": "Hello ModelHub"
        }
    ]
)

print(response.choices[0].message.content)
```

## Database

ModelHub uses SQLite for lightweight local storage.

The database is automatically initialized when the SDK is first configured.

Planned database entities:

- Providers
- Provider Credentials
- Models
- Model Capabilities
- Model Pricing
- Model Synchronization History
- API Tokens
- Request Logs
- Usage Statistics
- Application Settings

## Project Goals

1. Provide a unified interface for multiple AI providers.
2. Simplify API credential management.
3. Maintain an up-to-date catalogue of AI models.
4. Identify free-tier and paid models.
5. Provide a reusable Python SDK.
6. Expose OpenAI-compatible REST endpoints.
7. Support intelligent model selection and provider fallback.
8. Make AI integration easier across different applications and technologies.

## Roadmap

- [ ] Core architecture
- [ ] SQLite database initialization
- [ ] Provider registry
- [ ] Secure API key management
- [ ] Groq integration
- [ ] NVIDIA integration
- [ ] OpenRouter integration
- [ ] Automatic model discovery
- [ ] Free and paid model classification
- [ ] Unified chat completion interface
- [ ] Python SDK
- [ ] FastAPI REST gateway
- [ ] OpenAI-compatible API
- [ ] React management dashboard
- [ ] Usage tracking and analytics
- [ ] Provider fallback and intelligent routing
- [ ] Embeddings and multimodal support

## Security

- API keys must be encrypted before database storage.
- Master encryption keys must be stored separately from the database.
- Sensitive credentials must never appear in API responses or logs.
- ModelHub authentication tokens must be securely managed.
- Provider requests should use HTTPS.

## License

This project is licensed under the MIT License.
