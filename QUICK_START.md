# CivicAI - Quick Start Guide

Get CivicAI running locally in 5 minutes!

## 🚀 Fastest Setup (Docker)

### Prerequisites
- Docker & Docker Compose installed
- Gemini API Key from Google AI Studio (free)

### 1. Get Gemini API Key
```bash
# Visit: https://makersuite.google.com/app/apikey
# Copy your API key
```

### 2. Clone & Start
```bash
git clone https://github.com/civicai/ai-decision-platform.git
cd ai-decision-platform

# Copy environment template
cp backend/.env.example backend/.env

# Update Gemini API key in backend/.env
# GEMINI_API_KEY=your_api_key_here

# Start all services
docker-compose up -d

# Wait 30 seconds for services to start
sleep 30

# Open in browser
# Frontend: http://localhost:5173
# Backend API: http://localhost:8000
# API Docs: http://localhost:8000/docs
```

### 3. Stop Services
```bash
docker-compose down
```

---

## 📦 Manual Setup (Development)

### Backend Setup
```bash
cd backend

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Create .env file
cp .env.example .env
# Edit .env and add your Gemini API key

# Run server
uvicorn app:app --reload --host 0.0.0.0 --port 8000
```

### Frontend Setup
```bash
cd frontend

# Install dependencies
npm install

# Create .env file
cp .env.example .env
# Edit .env and add your Gemini API key and API URL

# Start development server
npm run dev

# Open http://localhost:5173 in browser
```

---

## 🧪 Test the Application

### 1. Test Chat Feature
- Open http://localhost:5173
- Ask: "I'm a farmer in Gujarat, what government schemes can help me?"
- AI should recommend PM-Kisan, NREGA, and other agricultural schemes

### 2. Test Dashboard
- Click "Dashboard" in sidebar
- View statistics and charts

### 3. Test API Directly
```bash
# Health check
curl http://localhost:8000/health

# Get all schemes
curl http://localhost:8000/api/schemes

# Send chat message
curl -X POST http://localhost:8000/api/chat \
  -H "Content-Type: application/json" \
  -d '{
    "user_id": 1,
    "message": "What schemes are available for small business?",
    "language": "en"
  }'

# Get scheme recommendations
curl -X POST http://localhost:8000/api/schemes/recommend \
  -H "Content-Type: application/json" \
  -d '{
    "user_profile": {
      "occupation": "farmer",
      "income": 300000,
      "state": "Gujarat",
      "age": 35
    },
    "language": "en"
  }'
```

---

## 📱 Key Features to Try

### 1. Chat Assistant
- Ask about government schemes
- Get AI-powered recommendations
- Rate responses (thumbs up/down)

### 2. Multi-Language
- Switch between English and Gujarati
- See real-time language support

### 3. Dashboard
- View platform statistics
- See your personal activity
- Check scheme categories

### 4. Scheme Information
- Click scheme names in chat
- View eligibility criteria
- See benefits and documents needed

---

## 🆘 Troubleshooting

### Issue: "Cannot connect to Gemini API"
**Solution**: 
- Verify Gemini API key in `.env`
- Check internet connection
- Visit https://makersuite.google.com/app/apikey to regenerate key

### Issue: "Port 8000 already in use"
**Solution**: 
```bash
# Kill process on port 8000
lsof -ti :8000 | xargs kill -9  # macOS/Linux
netstat -ano | findstr :8000   # Windows
```

### Issue: "Node modules not installing"
**Solution**:
```bash
cd frontend
rm -rf node_modules package-lock.json
npm install
```

### Issue: "Python virtual environment not activating"
**Solution**:
```bash
# Windows
venv\Scripts\activate.bat

# macOS/Linux alternative
python -m venv venv
source venv/bin/activate
```

---

## 📊 What to Explore

### Data in the System
- **5 Major Schemes** pre-loaded (PM-Kisan, PM Awas, APY, PMJDY, NREGA)
- **Dashboard** shows mock analytics
- **Chat** connects to Gemini AI

### Configuration Files
- `frontend/.env` - Frontend config
- `backend/.env` - Backend config
- `docker-compose.yml` - Docker setup

### Code Files
- `frontend/src/App.jsx` - Main React component
- `backend/app.py` - FastAPI server
- `frontend/src/components/ChatBot.jsx` - AI chat interface

---

## 🚀 Next Steps

### Production Deployment
Follow `docs/DEPLOYMENT.md` for Google Cloud deployment

### Database Setup
Replace in-memory database with PostgreSQL:
```bash
# In backend/.env
DATABASE_URL=postgresql://user:password@localhost:5432/civicai
```

### Add More Schemes
Edit `backend/app.py` and add to `GOVERNMENT_SCHEMES` array

### Customize UI
- Edit colors in `frontend/tailwind.config.js`
- Modify components in `frontend/src/components/`

---

## 📚 Documentation

- **Architecture**: `docs/ARCHITECTURE.md`
- **Deployment**: `docs/DEPLOYMENT.md`
- **API Docs**: http://localhost:8000/docs (when running)
- **README**: `README.md`

---

## 💡 Tips

1. **Use API Docs**: Visit http://localhost:8000/docs to explore all endpoints
2. **Check Logs**: `docker-compose logs -f` to see real-time logs
3. **Database**: Uses SQLite in dev, PostgreSQL in production
4. **Cache**: In-memory cache for schemes (no Redis needed)
5. **AI Model**: Uses Gemini Pro (free tier available)

---

## ⚙️ Configuration

### Change Port
```bash
# Frontend
cd frontend
npm run dev -- --port 3000

# Backend
uvicorn app:app --port 8001
```

### Enable Detailed Logging
```bash
# Backend .env
LOG_LEVEL=DEBUG
DEBUG=True
```

### Add More Schemes
Edit `GOVERNMENT_SCHEMES` in `backend/app.py`

---

## 🎓 Learning Resources

- React: https://react.dev
- FastAPI: https://fastapi.tiangolo.com
- Gemini AI: https://ai.google.dev
- Tailwind CSS: https://tailwindcss.com

---

## 📞 Support

- **Documentation**: Check `docs/` folder
- **Issues**: Review error messages in console/logs
- **API Questions**: Visit http://localhost:8000/docs
- **GitHub Issues**: [Report bugs](https://github.com/civicai/ai-decision-platform/issues)

---

**Happy Coding! 🚀**

Start with Docker Compose for the smoothest experience. Questions? Check the troubleshooting section above.
