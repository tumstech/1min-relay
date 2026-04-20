# 1min-Relay

## IMPORTANT - This is a forked Repo, source credit goes to Kokodev, Have preserved the original Readme for credit purpose.
This repo adds support for Code Generation, API currently supported by 1min.

## Overview
1min-Relay relays the 1min AI API to an OpenAI-compatible structure in under one minute. This project supports fast, reliable integration with various clients, features for managing conversation history and models, and optional hosted or self-hosted deployments. For details and updates, visit the hosted version and community channels below.

## Key links
- Hosted version: https://www.kokodev.cc/1minrelay
- Discord for support and updates: https://discord.gg/GQd3DrxXyj
- Donation: https://donate.stripe.com/00w4gB1NbdI60afcKPgMw00
- Paid hosted version and perks: https://shop.kokodev.cc/products
- GitHub repository: https://github.com/kokofixcomputers/1min-relay

## Features
- bolt.diy compatibility: Seamless integration with bolt.diy
- Conversation history: Preserve and manage conversations
- Broad client compatibility: Works with most clients that support an OpenAI Custom Endpoint
- Fast and reliable relay: Relays 1min AI API to an OpenAI-compatible structure quickly
- User-friendly: Easy to install and use
- Model exposure control: Expose all models or a predefined subset
- Streaming support: Real-time streaming for faster interactions
- Non-streaming support: Compatible with non-streaming workflows
- Docker support: Simple deployment with Docker
- Multi-document support: Upload and process documents (e.g., .docx, .pdf, .txt, .yaml, etc.)
- Image support: Upload and process images
- Code generation support: Generate code using AI models
- Architecture compatibility: ARM64 and AMD64 support
- Concurrent requests: Handles multiple requests simultaneously

## Paid perks (optional)
- Hosted service: Access anytime, anywhere
- Latest features: Early access to features not yet in the public version (e.g., image generation)
- Priority bug fixes: Faster resolution of common issues
- Priority support: Faster assistance compared to the public version

## Installation

### Bare-metal (local machine)
- Prerequisites: Python 3.x, pip, Git
- Clone the repository:
  - git clone https://github.com/kokofixcomputers/1min-relay.git
- Install dependencies:
  - pip install -r requirements.txt
- Run:
  - python3 main.py
  Note: On some systems, you may need to use python instead of python3.

### Docker (recommended for ease of deployment)

Pre-built images
- Pull the image:
  - docker pull kokofixcomputers/1min-relay:latest
- Create a dedicated network (recommended for memcached communication):
  - docker network create 1min-relay-network
- Start Memcached:
  - docker run -d --name memcached --network 1min-relay-network memcached
- Run the 1min-relay container:
  - docker run -d --name 1min-relay-container --network 1min-relay-network -p 5001:5001 \
    -e SUBSET_OF_ONE_MIN_PERMITTED_MODELS="mistral-nemo,gpt-4o-mini,deepseek-chat" \
    -e PERMIT_MODELS_FROM_SUBSET_ONLY=True \
    kokofixcomputers/1min-relay:latest

Environment variables
- SUBSET_OF_ONE_MIN_PERMITTED_MODELS: Subset of 1min.ai models to expose. Default: mistral-nemo,gpt-4o,deepseek-chat.
- PERMIT_MODELS_FROM_SUBSET_ONLY: Restrict model usage to the specified subset. Set to True to enforce, False to allow all models supported by 1min.ai. Default: True.

Self-build (Docker image from source)
1) Build the Docker image:
   - docker build -t 1min-relay:latest .
2) Create a dedicated network:
   - docker network create 1min-relay-network
3) Run Memcached:
   - docker run -d --name memcached --network 1min-relay-network memcached
4) Run the 1min-relay container:
   - docker run -d --name 1min-relay-container --network 1min-relay-network -p 5001:5001 \
     -e SUBSET_OF_ONE_MIN_PERMITTED_MODELS="mistral-nemo,gpt-4o-mini,deepseek-chat" \
     -e PERMIT_MODELS_FROM_SUBSET_ONLY=True \
     1min-relay:latest

Notes
- The container port 5001 is exposed to the host for API access.
- When using Docker Compose, you can simplify networking and service orchestration (see repository for a provided compose file).

Verification
- Check container logs:
  - docker logs -f 1min-relay-container
- Test the API endpoint (example):
  - curl -X GET http://localhost:5001/v1/models

### If you find this project useful, please consider starring the repository and supporting us through the provided donation or paid hosted options.
