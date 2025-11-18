# BürgerAuskunft: AI-Powered Civic Information Assistant

**BürgerAuskunft** (German for "Citizen Inquiry") is an open-source, speech-powered AI assistant designed to make public and civic information easily accessible to everyone. It leverages a powerful **Retrieval-Augmented Generation (RAG)** pipeline to provide accurate, transparent, and trustworthy answers from official documents.

Designed with a **privacy-first** and **security-by-design** philosophy, BürgerAuskunft runs entirely on self-hosted, open-source models, ensuring that user queries and sensitive institutional data never leave your control. Its intuitive, voice-driven chat interface allows users to ask questions in natural language and receive answers in real-time, transforming dense public records into an interactive and engaging resource.

The server component is implemented in Python, fully containerized with Docker for easy deployment, while the modern frontend is built with vanilla JavaScript/HTML.

## Table of Contents

-   [Features](#features)
-   [A Focus on Data Security](#a-focus-on-data-security)
-   [Architecture](#architecture)
-   [Prerequisites](#prerequisites)
-   [Getting Started](#getting-started)
-   [Configuration](#configuration)
-   [Usage](#usage)
-   [Development](#development)
-   [Contributing](#contributing)
-   [License](#license)

## Features

-   **End-to-End Voice Interaction**: A fully voice-driven experience, from asking questions to hearing the answers.
-   **Client-Side Speech Processing**: Speech recognition (Speech-to-Text) and synthesis (Text-to-Speech) are handled **entirely in the user's browser**, ensuring spoken queries are never sent to the server.
-   **Open-Source LLMs**: Utilizes powerful, locally-run open-source models (e.g., Llama 3, Phi-3) via Ollama, eliminating reliance on third-party APIs.
-   **High-Accuracy RAG Pipeline**: Employs advanced, multilingual embedding models and the LangChain framework to provide answers grounded in your specific documents, minimizing hallucinations.
-   **Real-Time Streaming Responses**: Communicates over WebSockets to stream answers back to the user token-by-token, creating a highly responsive "typing" effect.
-   **Fully Containerized**: The entire backend, including the LLM serving layer, is packaged in Docker for simple, reproducible, and scalable deployment.
-   **Modern Web Interface**: An intuitive and appealing chat interface for seamless user interaction.

## A Focus on Data Security

Data security and user privacy are core principles of the BürgerAuskunft architecture.

1.  **No Third-Party APIs**: By using self-hosted, open-source LLMs, the entire reasoning process happens on your own infrastructure. No user queries or document contents are ever sent to external companies.
2.  **Client-Side Speech Recognition**: The conversion of a user's voice into text happens directly in their browser using the Web Speech API. The server only ever receives the transcribed text, not the raw audio. This significantly enhances privacy.
3.  **Self-Contained Deployment**: The entire application stack, from the vector database to the LLM, is designed to run in a controlled environment. This makes it ideal for public institutions that cannot risk data exposure to external cloud services.

## Architecture

The system is designed as a modern, decoupled client-server application.

1.  **Client/Frontend**:
    -   Built with vanilla JavaScript/HTML.
    -   Handles all voice processing:
        -   **Speech Recognition**: Uses the browser's `webkitSpeechRecognition` API to convert the user's voice to text.
        -   **Speech Synthesis**: Uses the `SpeechSynthesisUtterance` API to convert the AI's text response back to speech.
    -   Communicates with the server via a persistent **WebSocket** connection for real-time, bidirectional messaging.

2.  **Server/Backend**:
    -   Implemented in Python using the FastAPI framework.
    -   Fully containerized with Docker and orchestrated with Docker Compose.
    -   Consists of two main services:
        -   **`BürgerAuskunft App`**: The main application that handles the RAG logic using LangChain, processes incoming queries, and streams responses.
        -   **`Ollama Service`**: A dedicated container that serves the open-source Large Language Model (e.g., Llama 3), providing powerful generative capabilities locally.

## Prerequisites

-   Docker and Docker Compose installed on the host machine.
-   For GPU acceleration (highly recommended): An NVIDIA GPU with the [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html) installed.
-   Poetry for Python dependency management during development.

## Getting Started


### 1. Connecting the Client

After the services are running, open the `index.html` file in the project root in a supported browser (like Google Chrome). The application will connect automatically, and you can start asking questions.
<img width="423" height="773" alt="2" src="https://github.com/user-attachments/assets/d5f786fd-1efd-4005-9647-c103e696f78d" />


### Frontend Development

The frontend is a single `index.html` file. Simply open it in your web browser to test changes.

## Contributing

Contributions are welcome! Please fork the repository and create a pull request with your changes.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
