
# Gemini Chatbot Backend (Oh_Mochi_AI)

This is the Spring Boot backend for the **Oh_Mochi_AI** chatbot. It provides a secure API for communicating with Google's Gemini 1.5 Flash model, handles user authentication via Google OAuth2, and manages frontend integration.

## 🚀 Features

* **Gemini AI Integration**: Connects to Google's `gemini-1.5-flash` model for generating chat responses.
* **Google OAuth2 Security**: Secure login and session management using Google accounts.
* **RESTful API**: Endpoints for sending messages, checking user status, and health monitoring.
* **CORS Configuration**: Pre-configured to work with local frontends (Vite/React) and cloud environments (GitHub Codespaces).
* **Error Handling**: Global exception handling for consistent API error responses.

## 🛠️ Tech Stack

* **Java**: 11
* **Framework**: Spring Boot 2.7.13
* **Build Tool**: Maven (Wrapper included)
* **Security**: Spring Security & OAuth2 Client
* **AI**: Google Generative AI (Gemini) REST API

## 📋 Prerequisites

* Java Development Kit (JDK) 11 or higher.
* A Google Cloud Project with:
    * **Gemini API Key** enabled.
    * **OAuth 2.0 Credentials** (Client ID and Secret) set up.

## ⚙️ Configuration & Environment Variables

The application relies on environment variables for sensitive credentials. You must set these before running the application.

Create a `.env` file or export these variables in your terminal/IDE:

| Variable | Description | Example |
| :--- | :--- | :--- |
| `GEMINI_API_KEY` | Your Google Gemini API Key | `AIzaSyD...` |
| `GOOGLE_CLIENT_ID` | OAuth2 Client ID from Google Cloud Console | `1234...apps.googleusercontent.com` |
| `GOOGLE_CLIENT_SECRET` | OAuth2 Client Secret from Google Cloud Console | `GOCSPX-...` |
| `FRONTEND_URL` | URL of your frontend app (for redirects/CORS) | `http://localhost:8080` |

> **Note:** The backend runs on port **8081** by default.

## 🏃‍♂️ How to Run

1.  **Clone the repository**:
    ```bash
    git clone <repository-url>
    cd gemini-chatbot-backend/gemini-chatbot
    ```

2.  **Build the project**:
    ```bash
    ./mvnw clean install
    ```

3.  **Run the application**:
    ```bash
    ./mvnw spring-boot:run
    ```

Alternatively, you can skip tests for a faster start:
```bash
./mvnw spring-boot:run -DskipTests

```

## 🔌 API Endpoints

See the `FRONTEND_INTEGRATION.md` file for detailed integration examples.

### Core Endpoints

| Method | Endpoint | Description |
| --- | --- | --- |
| **GET** | `/api/chat/health` | Check if the backend is running. |
| **POST** | `/api/chat/message` | Send a JSON message to Gemini. Requires Auth. |
| **GET** | `/api/chat/user` | Get currently logged-in user details. |
| **GET** | `/login/oauth2/code/google` | OAuth callback (handled by browser). |

### Request Example (Send Message)

**POST** `http://localhost:8081/api/chat/message`

```json
{
  "message": "Hello, how are you?"
}

```

## 🔒 Security & CORS

* **Authentication**: The app uses cookie-based sessions (`JSESSIONID`). Ensure your frontend request includes `credentials: 'include'` or `withCredentials: true`.
* **CORS**: Configured in `SecurityConfig.java`. It currently allows **all origins** (`*`) to facilitate development in environments like GitHub Codespaces.
* *Production Note:* For a production deployment, update `SecurityConfig.java` to restrict allowed origins to your specific domain.



## 🐛 Troubleshooting

* **500 Errors**: Check your `GEMINI_API_KEY` and ensure the Google Generative AI API is enabled in your cloud console.
* **CORS Errors**: Verify `FRONTEND_URL` matches your frontend's address.
* **Login Loops**: Ensure your Google Cloud Console "Authorized redirect URIs" includes `http://localhost:8081/login/oauth2/code/google`.

## 📁 Project Structure

* `src/main/java/com/chatbot/config`: Security and CORS configuration.
* `src/main/java/com/chatbot/controller`: API endpoint definitions.
* `src/main/java/com/chatbot/service`: Logic for calling the Gemini API.
* `src/main/java/com/chatbot/dto`: Data Transfer Objects for requests/responses.
* `FRONTEND_INTEGRATION.md`: Guide for connecting a React/Vite frontend.

```

```
