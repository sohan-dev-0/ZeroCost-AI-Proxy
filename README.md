# Develop AI applications locally with zero API costs and transition to production by changing a single string.
# PFFAI Local Proxy is a macOS-exclusive, OpenAI-compatible gateway that leverages your Gemini browser session to eliminate development-stage billing.

## 1. Executive Overview
PFFAI Local Proxy is a desktop application engineered for software developers who require extensive API testing without incurring financial overhead. The application runs a local HTTP server that mimics the official OpenAI API structure. Instead of routing requests through a paid API key, it securely routes them through a local browser session using Google Gemini.

This architecture allows developers to build, test, and iterate on AI-powered features for free. When the application is ready for production, developers do not need to rewrite their backend logic. By simply replacing the local base URL with the official OpenAI or Gemini endpoint and injecting a valid API key, the application seamlessly transitions to production.

**Current System Constraints:**
1. Operating System: macOS only.
2. AI Provider Support: Google Gemini (via browser session automation).
3. API Format: OpenAI-compatible endpoints.

## 2. The "Zero to Production" Workflow
The primary advantage of this proxy is its drop-in compatibility with the OpenAI SDK. The following Python example demonstrates the transition from local development to production deployment.

```python
# 1. Local Development Environment (Zero Cost)
client = OpenAI(
    base_url="http://localhost:13337/v1/chat/completions",
    api_key="any-dummy-key" 
)

# 2. Production Environment (Official Billing)
# To deploy, change the base_url and api_key. No other logic changes are required.
client = OpenAI(
    base_url="https://api.openai.com/v1",
    api_key="sk-your-real-openai-api-key"
)
```

## 3. Detailed Feature Architecture

**Zero Token Cost Engine:** The application intercepts API requests and utilizes an active, automated browser session to generate responses. A built-in dashboard tracks the estimated financial savings based on token consumption, providing real-time feedback on development cost reduction.

**OpenAI API Compatibility:** The proxy strictly adheres to the standard `/v1/chat/completions` endpoint format. It correctly parses standard JSON payloads, including roles, message history, and model parameters, ensuring that existing SDKs and HTTP clients function without modification.

**Dynamic Persona Routing:** Unlike standard proxies, PFFAI allows the creation of custom, task-specific endpoints. For instance, a request routed to `/v1/python` is automatically injected with a system prompt defining the AI as a "Principal Python Architect." Other custom routes can be defined for specific architectural tasks, database optimization (SQL), or general chat, ensuring the model adopts the correct context without repetitive prompt engineering from the client side.

**Local Network (Wi-Fi) Accessibility:** The gateway is not restricted to localhost. It binds to the local network IP address (e.g., 192.168.x.x:13337). This enables developers to test mobile applications on physical iOS or Android devices, or connect frontend frameworks running on different devices, directly to the local AI proxy.

**Anti-Echo Isolation Protocol:** Standard browser automation often results in the AI repeating the system prompt or outputting internal "thinking" markers. This proxy utilizes an isolation layer that filters out prompt echoes and internal processing artifacts, returning only the clean, final assistant response to the API client.

**Full Response Drain Mechanism:** To prevent truncated or incomplete JSON payloads, the proxy implements a full drain mechanism. It ensures that the connection remains open until 100% of the generated tokens are received and compiled, preventing timeout errors during long-form generation.

## 4. Installation and Quick Start (macOS)

1. Navigate to the Releases section on the right sidebar of this repository.
2. Download the latest `.dmg` file for macOS.
3. Open the downloaded file and drag the PFFAI application into your Applications folder.
4. Launch the application from your Applications folder or Launchpad.
5. Verify that the Gateway toggle switch is in the ON position. The default port is set to 13337.
6. If testing from external devices, ensure the Wi-Fi Access toggle is enabled and note the provided local IP address.
7. Open your API client (such as Postman, Insomnia, or a cURL terminal command) and direct requests to http://localhost:13337/v1/chat/completions.
8. Ensure the JSON payload includes the model parameter set to "auto" or points to a specific custom route.

## 5. Interface Documentation

*(Insert your application screenshots here by dragging and dropping them into this section)*

**Image 1:** The main chat interface, demonstrating the prompt input, clean output generation, and the real-time cost savings tracker.
**Image 2:** The API Gateway dashboard, displaying active routes, port configurations, and Wi-Fi network binding.
**Image 3:** A terminal or API client (Postman) view, verifying the JSON response structure from the local endpoint.

## 6. System Requirements and Prerequisites

1. macOS operating system (Apple Silicon or Intel).
2. An active Google account with access to Gemini.
3. Familiarity with HTTP requests and API integration.

## 7. Important Disclaimers and Best Practices

**Terms of Service Compliance:** This application is strictly designed for local development, prototyping, and educational purposes. It relies on browser automation, which may violate the Terms of Service (ToS) of the AI provider if used for automated, high-volume scraping or production workloads.

**Account Security:** Because the application utilizes browser sessions, there is an inherent risk of account flagging or suspension. It is highly recommended to use a secondary or burner Google account during the use of this tool. Do not use your primary or corporate Google account.

**Network Security:** This tool exposes a local HTTP server. While intended for local area networks, users should ensure they are operating on trusted, secure Wi-Fi networks. The server should not be exposed to the public internet.

**VirusTotal Verification:** [Insert your VirusTotal scan link here to verify the .dmg file is free of malware]

---
If this tool assists in reducing your development costs, please consider starring this repository.
