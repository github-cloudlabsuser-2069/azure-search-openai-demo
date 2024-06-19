# Backend Documentation

The backend of the application is located in the [`app/backend`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2FC%3A%2FUsers%2Fazureuser%2Fazure-search-openai-demo%2Fapp%2Fbackend%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "c:\Users\azureuser\azure-search-openai-demo\app\backend") directory.

## Overview

The backend is built using [Quart](https://quart.palletsprojects.com/), a Python framework for asynchronous web applications. It communicates with the frontend using the [AI Chat App HTTP Protocol](https://github.com/Azure-Samples/ai-chat-app-protocol).

## Key Components

### Approaches

The [`app/backend/approaches`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2FC%3A%2FUsers%2Fazureuser%2Fazure-search-openai-demo%2Fapp%2Fbackend%2Fapproaches%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "c:\Users\azureuser\azure-search-openai-demo\app\backend\approaches") folder contains the classes powering the Chat and Ask tabs. Each class uses a different RAG (Retrieval Augmented Generation) approach, which include system messages that should be changed to match your data.

#### Chat Approach

The chat tab uses the approach programmed in [chatreadretrieveread.py](https://github.com/Azure-Samples/azure-search-openai-demo/blob/main/app/backend/approaches/chatreadretrieveread.py). This approach involves the following steps:

1. It calls the OpenAI ChatCompletion API (with a temperature of 0) to turn the user question into a good search query.
2. It queries Azure AI Search for search results for that query (optionally using the vector embeddings for that query).
3. It then combines the search results and original user question, and calls the OpenAI ChatCompletion API (with a temperature of 0.7) to answer the question based on the sources. It includes the last 4K of message history as well (or however many tokens are allowed by the deployed model).

The `system_message_chat_conversation` variable is currently tailored to the sample data since it starts with "Assistant helps the company employees with their healthcare plan questions, and questions about the employee handbook." Change that to match your data.

## Running the Backend Locally

You can only run the backend locally **after** having successfully run the `azd up` command. If you haven't yet, follow the steps in [Azure deployment](../README.md#azure-deployment) above.

1. Run `azd auth login`
2. Change dir to [`app`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2FC%3A%2FUsers%2Fazureuser%2Fazure-search-openai-demo%2Fapp%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "c:\Users\azureuser\azure-search-openai-demo\app")
3. Run `./start.ps1` or `./start.sh` or run the "VS Code Task: Start App" to start the project locally.

When you run `./start.ps1` or `./start.sh`, the backend files will be watched and reloaded automatically.