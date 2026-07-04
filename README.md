# 🏛️ CivicAI - AI Decision Intelligence Platform

**Empowering Citizens with AI-Powered Government Scheme Intelligence**

An intelligent platform that uses Google's Gemini AI to help citizens discover, understand, and apply for relevant government schemes across India.

---

## 📋 Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Installation & Setup](#installation--setup)
- [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [Environment Variables](#environment-variables)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [License](#license)

---

## ✨ Features

### 🤖 AI-Powered Chat Assistant
- Real-time conversation with Gemini AI
- Intelligent scheme recommendations based on user profile
- Support for English and Gujarati languages
- Context-aware responses

### 🏛️ Government Scheme Database
- **500+ government schemes** indexed and searchable
- Eligibility criteria, benefits, and application process
- Real-time scheme recommendations
- Multi-category support (Agricultural, Healthcare, Housing, Education, Social Security, etc.)

### 📊 Intelligent Dashboard
- User activity analytics
- Scheme exploration tracking
- Monthly trends and statistics
- Success metrics

### 🌐 Multi-Language Support
- English
- Gujarati (ગુજરાતી)
- Extensible to other Indian languages

### 📱 Responsive Design
- Mobile-first approach
- Works seamlessly on all devices
- Progressive Web App ready

### 🔐 Secure & Privacy-First
- End-to-end encryption ready
- No data storage without consent
- GDPR-compliant architecture

---

## 🛠️ Tech Stack

### Frontend
- **React 18** - UI framework
- **Vite** - Build tool
- **Tailwind CSS** - Styling
- **Recharts** - Data visualization
- **Lucide React** - Icons
- **Axios** - HTTP client

### Backend
- **FastAPI** - Python web framework
- **Uvicorn** - ASGI server
- **SQLAlchemy** - ORM
- **PostgreSQL** - Database
- **Google Gemini AI** - LLM
- **Google Cloud** - Infrastructure

### DevOps & Deployment
- **Docker** - Containerization
- **Docker Compose** - Multi-container orchestration
- **Google Cloud Run** - Serverless deployment
- **GitHub Actions** - CI/CD

---

## 📁 Project Structure

```
ai-decision-platform/
│
├── frontend/                          # React Frontend
│   ├── src/
│   │   ├── components/               # React Components
│   │   │   ├── Navbar.jsx            # Navigation bar
│   │   │   ├── Sidebar.jsx           # Sidebar navigation
│   │   │   ├── ChatBot.jsx           # AI Chat component
│   │   │   └── Dashboard.jsx         # Analytics dashboard
│   │   ├── pages/                    # Page components
│   │   ├── services/
│   │   │   ├── gemini.js            # Gemini AI integration
│   │   │   └── api.js               # API client
│   │   ├── assets/                  # Static assets
│   │   ├── App.jsx                  # Main app component
│   │   ├── main.jsx                 # React entry point
│   │   └── index.css                # Global styles
│   ├── public/                       # Public assets
│   ├── package.json
│   ├── vite.config.js
│   ├── tailwind.config.js
│   └── .env
│
├── backend/                          # FastAPI Backend
│   ├── app.py                       # Main application
│   ├── config.py                    # Configuration
│   ├── requirements.txt             # Python dependencies
│   ├── services/                    # Business logic
│   │   ├── gemini.py               # AI service
│   │   ├── schemes.py              # Scheme service
│   │   └── analytics.py            # Analytics service
│   └── .env
│
├── docs/                             # Documentation
│   ├── ARCHITECTURE.md              # System architecture
│   ├── API.md                       # API documentation
│   └── DEPLOYMENT.md                # Deployment guide
│
├── Dockerfile                        # Backend Docker image
├── docker-compose.yml               # Multi-container setup
├── .github/
│   └── workflows/                   # CI/CD pipelines
│       └── deploy.yml               # GitHub Actions
│
├── README.md                         # This file
└── LICENSE                           # MIT License
```

---

## 🚀 Installation & Setup

### Prerequisites
- Node.js 18+ and npm/yarn
- Python 3.11+
- PostgreSQL 13+
- Docker and Docker Compose (optional)
- Google Gemini API Key (free)

### 1. Clone Repository
```bash
git clone https://github.com/civicai/ai-decision-platform.git
cd ai-decision-platform
```

### 2. Frontend Setup
```bash
cd frontend

# Install dependencies
npm install

# Create .env file
cp .env.example .env

# Update .env with your Gemini API key
# VITE_GEMINI_API_KEY=your_api_key_here
```

### 3. Backend Setup
```bash
cd ../backend

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Create .env file
cp .env.example .env

# Update .env with your database URL and API keys
# DATABASE_URL=postgresql://user:password@localhost:5432/civicai
# GEMINI_API_KEY=your_api_key_here
```

---

## 🏃 Running the Application

### Option 1: Local Development

**Terminal 1 - Backend:**
```bash
cd backend
source venv/bin/activate
uvicorn app:app --reload --host 0.0.0.0 --port 8000
```

**Terminal 2 - Frontend:**
```bash
cd frontend
npm run dev
```

Access the application:
- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:8000
- **API Docs**: http://localhost:8000/docs

### Option 2: Docker Compose

```bash
# Build and start all services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

---

## 📚 API Documentation

### Base URL
```
http://localhost:8000/api
```

### Key Endpoints

#### Health Check
```http
GET /health
```

#### Chat with AI
```http
POST /api/chat
Content-Type: application/json

{
  "user_id": 1,
  "message": "I'm a farmer, what schemes can help me?",
  "language": "en"
}
```

#### Get Schemes
```http
GET /api/schemes?category=Agricultural&limit=10
```

#### Scheme Recommendations
```http
POST /api/schemes/recommend
Content-Type: application/json

{
  "user_profile": {
    "occupation": "farmer",
    "income": 250000,
    "state": "Gujarat"
  },
  "language": "en"
}
```

#### Dashboard Stats
```http
GET /api/dashboard/stats
```

For complete API documentation, visit: http://localhost:8000/docs

---

## 🔑 Environment Variables

### Frontend (.env)
```env
VITE_GEMINI_API_KEY=your_gemini_api_key
VITE_API_URL=http://localhost:8000/api
VITE_APP_NAME=CivicAI
VITE_APP_VERSION=1.0.0
```

### Backend (.env)
```env
GEMINI_API_KEY=your_gemini_api_key
DATABASE_URL=postgresql://user:password@localhost:5432/civicai
GOOGLE_CLOUD_PROJECT=your-project-id
SECRET_KEY=your-secret-key
ENVIRONMENT=development
DEBUG=True
```

---

## 🌐 Deployment

### Google Cloud Run

1. **Build and push Docker image:**
```bash
gcloud builds submit --tag gcr.io/PROJECT_ID/civicai-backend
```

2. **Deploy to Cloud Run:**
```bash
gcloud run deploy civicai-backend \
  --image gcr.io/PROJECT_ID/civicai-backend \
  --platform managed \
  --region us-central1 \
  --set-env-vars GEMINI_API_KEY=your_key,DATABASE_URL=your_db_url
```

3. **Deploy Frontend to Firebase:**
```bash
cd frontend
npm run build
firebase deploy
```

### Vercel (Frontend)

```bash
cd frontend
vercel
```

---

## 📊 Key Features Explained

### 1. AI Chat Assistant
- Uses Google's Gemini Pro model
- Understands user context and needs
- Recommends relevant government schemes
- Supports multi-language conversations

### 2. Scheme Recommendation Engine
- Analyzes user profile (occupation, income, age, etc.)
- Matches against 500+ government schemes
- Provides eligibility criteria
- Shows application process and benefits

### 3. Dashboard Analytics
- Tracks user queries and interactions
- Shows scheme popularity
- Displays application success rates
- Monthly trends and insights

### 4. Multi-Language Support
- English (Default)
- Gujarati (ગુજરાતી)
- Extensible architecture for adding more languages

---

## 🧪 Testing

### Frontend Tests
```bash
cd frontend
npm run test
```

### Backend Tests
```bash
cd backend
pytest
```

---

## 🤝 Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open Pull Request

---

## 📄 License

This project is licensed under the MIT License - see LICENSE file for details.

---

## 🙏 Acknowledgments

- Google Gemini AI for powering the intelligence
- Indian Government for publishing scheme information
- Open source community for excellent libraries and tools

---

## 📞 Support

- **Documentation**: [docs/](./docs/)
- **Issues**: [GitHub Issues](https://github.com/civicai/ai-decision-platform/issues)
- **Email**: support@civicai.in
- **Website**: https://civicai.in

---

## 🚀 Roadmap

- [ ] Integration with official government portals
- [ ] Real-time application status tracking
- [ ] Video tutorials for scheme applications
- [ ] Mobile app (React Native)
- [ ] Voice chat support
- [ ] Document upload and verification
- [ ] Payment integration
- [ ] Integration with state-specific schemes
- [ ] SMS and email notifications
- [ ] Offline mode

---

**Made with ❤️ for Citizens of India**

**Version**: 1.0.0  
**Last Updated**: July 2026  
**Status**: Active Development
