# RAG-Agent: Retrieval-Augmented Generation with Agent Capabilities
A modular, production-ready framework for building intelligent LLM applications that combine **Retrieval-Augmented Generation (RAG)** for factual accuracy and **Agent** for autonomous decision-making.

## Overview
RAG-Agent integrates RAG (to mitigate LLM hallucinations with grounded knowledge retrieval) and Agent (powered by the REACT paradigm for "Reason-Act-Observe" workflows) to create robust, context-aware AI applications. The framework is designed with modularity, configurability, and ease of deployment in mind, making it suitable for building enterprise-grade QA systems, knowledge base assistants, automated decision tools, and more.

## Core Features
- **Modular Architecture**: Decoupled layers for RAG, Agent, model management, and tooling for easy extension.
- **Retrieval-Augmented Generation**: Lightweight local Chroma vector database for knowledge retrieval (no complex cloud dependencies).
- **Autonomous Agent**: REACT-based agent implementation with customizable tool sets (retrieval, calculation, API calls, etc.).
- **Configuration-Driven**: Core parameters (model settings, vector DB config, agent rules) managed via YAML files (no code changes required).
- **Production-Grade Engineering**: Standardized logging, config handling, prompt management, and file/path utilities.
- **Model Agnostic**: Unified model factory to seamlessly switch between LLMs (OpenAI, open-source models, Chinese domestic LLMs, etc.).

## Directory Structure
```
RAG-Agent/
├── app.py                # Entry point for running the RAG-Agent application
├── agent/                # Core Agent module
│   ├── react_agent.py    # REACT paradigm agent implementation
│   ├── tools/            # Agent toolset (external tool integrations)
│   └── chroma/           # Chroma vector DB local storage helpers
├── config/               # YAML configuration files
│   ├── agent.yml         # Agent behavior/rule configuration
│   ├── chroma.yml        # Chroma vector database settings
│   ├── prompts.yml       # Prompt template configurations
│   └── rag.yml           # RAG pipeline parameters
├── model/                # Model management layer
│   └── factory.py        # Model factory for unified LLM instantiation
├── rag/                  # RAG core logic (retrieval, recall, context assembly)
├── utils/                # Utility modules (shared core functionality)
│   ├── config_handler.py # Load and parse YAML configurations
│   ├── file_handler.py   # General file operation utilities
│   ├── logger_handler.py # Standardized logging (date-based log files)
│   ├── path_tool.py      # Path management helpers
│   └── prompt_loader.py  # Load and render prompt templates
├── chroma_db/            # Chroma vector DB local storage (sqlite3)
├── data/                 # Raw data storage for knowledge base ingestion
├── prompts/              # Prompt template files
├── logs/                 # Date-based log files (e.g., agent_20260125.log)
└── README.md             # Project documentation
```

## Key Components
### 1. Retrieval-Augmented Generation (RAG)
- **Chroma Vector Database**: Lightweight, local vector store for embedding and retrieving knowledge base data (configured in `config/chroma.yml`).
- **RAG Pipeline**: The `rag/` directory handles end-to-end retrieval logic (embedding, similarity search, context stitching) to ground LLMs in factual data.

### 2. Agent System
- **REACT Agent**: Implemented in `agent/react_agent.py`, the agent follows the REACT paradigm to reason about user requests, select appropriate tools, and observe outcomes.
- **Customizable Tools**: Extend the `agent/tools/` directory to add custom tools (e.g., API integrations, calculators, web scrapers) for the agent to use.

### 3. Engineering Foundations
- **Config Management**: `utils/config_handler.py` loads all YAML configurations, enabling dynamic adjustments without code changes.
- **Logging**: `utils/logger_handler.py` generates structured, date-based logs in the `logs/` directory for debugging and monitoring.
- **Prompt Management**: `utils/prompt_loader.py` loads templates from the `prompts/` directory, supporting dynamic prompt stitching for LLMs.
- **Model Factory**: `model/factory.py` provides a unified interface for initializing different LLMs, simplifying model switching.

## Use Cases
- Enterprise knowledge base QA systems (internal docs, product manuals)
- Intelligent customer service bots (grounded in company data)
- Industry-specific assistants (finance, healthcare, education)
- Automated office assistants (decision support, data retrieval)
- Context-aware chatbots with factual accuracy

## Getting Started
### Prerequisites
- Python 3.9+
- Chroma DB (`pip install chromadb`)
- LLM SDKs (e.g., openai, dashscope, etc., based on your chosen model)
- Additional dependencies (install via `pip install -r requirements.txt` – create a `requirements.txt` with: `pyyaml`, `python-dotenv`, `chromadb`, `openai`, `loguru`)

### Basic Setup
1. **Configure Parameters**: Update YAML files in the `config/` directory to set your LLM API keys, Chroma DB settings, agent rules, and RAG parameters.
2. **Ingest Knowledge Base**: Add raw data (text, docs) to the `data/` directory and run the RAG ingestion pipeline (extend `rag/` to support your data format).
3. **Launch the Application**: Run the main entry point:
   ```bash
   python app.py
   ```

## Customization
- **Add New Tools**: Extend the `agent/tools/` directory with custom tool classes and register them in `config/agent.yml`.
- **Switch LLMs**: Update `model/factory.py` to support new LLMs and configure the model name/parameters in `config/rag.yml` or `config/agent.yml`.
- **Modify Prompt Templates**: Update files in the `prompts/` directory to align with your use case (e.g., QA, summarization, decision-making).

## License
This project is licensed under the MIT License - see the LICENSE file for details.

## Contributing
Contributions are welcome! Please open an issue to discuss feature requests or bug fixes, and submit pull requests with clear documentation of changes.

## Acknowledgments
- Chroma DB for lightweight vector storage
- REACT paradigm for agent design
- Open-source LLM ecosystems for model integration
