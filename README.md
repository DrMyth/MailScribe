# MailScribe - AI Email Reply Generator

A comprehensive full-stack application that leverages Google's Gemini AI to generate intelligent email replies. The project includes a Spring Boot backend, React frontend, and Chrome extension for seamless Gmail integration.

## Features

### Core Functionality
- **AI-Powered Email Generation** using Google Gemini API
- **Multiple Tone Options**: Professional, Casual, Friendly
- **Real-time Email Processing** with responsive UI
- **Gmail Integration** via Chrome extension
- **Copy-to-Clipboard** functionality
- **Cross-Platform Support** (Web app + Browser extension)

### Technical Features
- **RESTful API** with Spring Boot
- **Modern React** with Material-UI components
- **Chrome Extension** with Gmail DOM manipulation
- **CORS-enabled** for seamless frontend-backend communication
- **Error Handling** and loading states
- **Environment-based Configuration**

## Architecture

```
Email Writer Project
├── backend/        # Spring Boot Backend (Port: 8081)
├── frontend/       # React Frontend (Port: 5173)
├── extension/      # Chrome Extension
└── README.md       # Project Documentation
```

### System Architecture
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   React Web App │    │ Chrome Extension│    │  Spring Boot API│
│   (Port: 5173)  │◄──►│   (Gmail DOM)   │◄──►│   (Port: 8081)  │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                                        │
                                                        ▼
                                               ┌─────────────────┐
                                               │   Gemini AI API │
                                               └─────────────────┘
```

## Prerequisites

- **Java 23** or higher
- **Node.js 18+** and npm
- **Google Gemini API Key** ([Get it here](https://aistudio.google.com/))
- **Chrome Browser** (for extension)
- **Maven** (included via wrapper)

## Quick Start

### 1. Clone & Setup
```bash
git clone <your-repository-url>
cd email-writer
```

### 2. Environment Configuration
Create environment variables for the Gemini API:

**Windows (PowerShell):**
```powershell
$env:GEMINI_URL="https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent?key="
$env:GEMINI_KEY="your_gemini_api_key_here"
```

**Linux/Mac:**
```bash
export GEMINI_URL="https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent?key="
export GEMINI_KEY="your_gemini_api_key_here"
```

### 3. Start Backend (Spring Boot)
```bash
cd email-writer-sb
./mvnw spring-boot:run
# Windows: mvnw.cmd spring-boot:run
```
Backend will be available at: `http://localhost:8081`

### 4. Start Frontend (React)
```bash
cd email-writer-react
npm install
npm run dev
```
Frontend will be available at: `http://localhost:5173`

### 5. Install Chrome Extension
1. Open Chrome and go to `chrome://extensions/`
2. Enable "Developer mode"
3. Click "Load unpacked"
4. Select the `email-writer-ext` folder
5. Extension will appear in your toolbar

## Detailed Setup

### Backend Setup (Spring Boot)

The backend is a Spring Boot application that provides REST API endpoints for email generation.

**Key Configuration:**
- **Port**: 8081
- **Main Class**: `EmailWriterSbApplication`
- **API Endpoint**: `POST /api/email/generate`

**Dependencies:**
- Spring Boot Web
- Spring Boot WebFlux
- Jackson (JSON processing)

**Run Commands:**
```bash
cd email-writer-sb

# Development
./mvnw spring-boot:run

# Build JAR
./mvnw clean package
java -jar target/email-writer-sb-0.0.1-SNAPSHOT.jar

# Run tests
./mvnw test
```

### Frontend Setup (React)

Modern React application with Material-UI for professional styling.

**Features:**
- Material-UI components
- Axios for API calls
- Responsive design
- Loading states and error handling

**Available Scripts:**
```bash
cd email-writer-react

# Install dependencies
npm install

# Development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Lint code
npm run lint
```

### Chrome Extension Setup

Gmail-integrated Chrome extension that adds an "AI Reply" button to the compose window.

**Features:**
- Manifest V3 compatibility
- Gmail DOM integration
- Auto-content detection
- Direct reply insertion

**Installation:**
1. Open Chrome Extensions: `chrome://extensions/`
2. Enable Developer mode
3. Load unpacked extension from `email-writer-ext` folder

## API Documentation

### POST /api/email/generate

Generate an AI-powered email reply based on the original email content.

**Request:**
```json
{
  "emailContent": "Original email content here...",
  "tone": "professional"
}
```

**Response:**
```json
"Generated email reply content..."
```

**Tone Options:**
- `professional` - Formal business communication
- `casual` - Relaxed, friendly tone
- `friendly` - Warm and approachable
- `null` or empty - Default tone

**Example Usage:**
```javascript
const response = await fetch('http://localhost:8081/api/email/generate', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    emailContent: 'Thank you for your inquiry about our services...',
    tone: 'professional'
  })
});

const reply = await response.text();
```

## Development

### Project Structure
```
email-writer-sb/
├── src/main/java/com/email/writer/
│   ├── EmailWriterSbApplication.java
│   └── app/
│       ├── EmailGeneratorController.java
│       ├── EmailGeneratorService.java
│       └── EmailRequest.java
├── src/main/resources/
│   └── application.properties
└── pom.xml

email-writer-react/
├── src/
│   ├── App.jsx
│   ├── App.css
│   └── main.jsx
├── package.json
└── vite.config.js

email-writer-ext/
├── manifest.json
├── content.js
└── content.css
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## Support

For issues and feature requests, please create an issue in the repository.

⭐ **Star this repository if you found it helpful!** 