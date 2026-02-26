# 🎓 AI-Powered Smart Study Planner

## 📋 Project Overview

A comprehensive AI-based intelligent study planning system that automatically generates personalized timetables, identifies weak topics, generates AI notes, and provides real-time analytics for exam preparation.

---

## 🏗️ System Architecture

### Frontend
- **HTML/CSS/JavaScript** (Current: my/ folder)
- **React** (Planned for advanced version)
- Login/Register
- Syllabus Upload
- Interactive Dashboard
- Progress Analytics
- Pomodoro Timer

### Backend
- **Node.js + Express** (backend/server.js)
- **Python Flask** (Fallback: app.py)
- JWT Authentication
- Timetable Algorithm
- AI Integration

### AI Layer
- **OpenAI API** Integration
- Weak Topic Detection
- Notes Generation
- Smart Revision Scheduling

### Database
- **MongoDB** (Prepared schemas)
- Collections: Users, Subjects, Timetables, StudySessions, Analytics

---

## 🧠 Core Algorithms

### 1. Timetable Generation Algorithm
**Logic:**
```
1. Sort topics by difficulty (Hard → Easy)
2. Calculate available days until exam
3. Distribute topics proportionally
4. Apply spaced repetition every 3 days
5. Schedule full revision week before exam
6. Auto-adjust based on progress
```

**File:** `backend/services/TimetableGenerator.js`

### 2. Weak Topic Identification
**Algorithm:**
```
WeakScore = (LowQuizScore × 0.5) + (HighTimeTaken × 0.3) + (IncompleteSessions × 0.2)
```

**Factors:**
- Low quiz performance
- Excessive time spent
- Incomplete study sessions

**File:** `backend/services/WeakTopicAnalyzer.js`

### 3. Exam Readiness Score
**Formula:**
```
Readiness = (CompletedTopics / TotalTopics) × 100 × QualityFactor
```

**Quality Adjustment:**
- Based on average weakness score
- Considers quiz scores
- Factors in revision completion

**File:** `backend/services/AnalyticsService.js`

### 4. AI Notes Generation
**Uses OpenAI API** to generate:
- Concise revision notes
- Key concepts and formulas
- Real-world applications
- Common mistakes
- Practice tips

**File:** `backend/services/AINotesGenerator.js`

---

## 📂 Folder Structure

```
Smart-study-planner/
├── backend/
│   ├── models/
│   │   ├── User.js
│   │   ├── Subject.js
│   │   ├── Timetable.js
│   │   ├── StudySession.js
│   │   └── Analytics.js
│   ├── services/
│   │   ├── TimetableGenerator.js
│   │   ├── WeakTopicAnalyzer.js
│   │   ├── AINotesGenerator.js
│   │   └── AnalyticsService.js
│   ├── routes/
│   ├── controllers/
│   ├── utils/
│   ├── server.js
│   └── package.json
├── frontend/
│   ├── Components/
│   ├── Pages/
│   ├── Services/
│   └── App.js
├── my/
│   ├── index.html
│   ├── login.html
│   ├── register.html
│   ├── dashboard.html
│   ├── login.js
│   ├── register.js
│   ├── dashboard.js
│   ├── pomodoro.js
│   ├── api.js
│   └── style.css
├── app.py (Python Flask Backend - Fallback)
├── package.json
├── .env
└── .gitignore
```

---

## 🚀 Getting Started

### Prerequisites
- Node.js v14+
- Python 3.8+ (for fallback backend)
- MongoDB Atlas Account (for database)
- OpenAI API Key (for AI features)

### Installation

1. **Clone/Setup Project**
```bash
cd Smart-study-planner
```

2. **Install Backend Dependencies**
```bash
npm install
```

3. **Setup Environment Variables**
```bash
# .env file
PORT=5000
JWT_SECRET=your_secret_key_here
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/smart-planner
OPENAI_API_KEY=sk-...your-key-here...
NODE_ENV=development
```

4. **Run Backend (Node.js)**
```bash
npm start
# or for development
npm run dev
```

5. **Or Run Backend (Python Flask)**
```bash
python app.py
```

6. **Open Frontend**
```bash
# Open my/index.html in browser
# Or (when React is set up)
cd frontend
npm install
npm start
```

---

## 📡 API Endpoints

### Authentication
```
POST   /api/auth/register      - Register new user
POST   /api/auth/login         - Login user
GET    /api/user/profile       - Get user profile
PUT    /api/user/profile       - Update profile settings
```

### Subject Management
```
POST   /api/subjects           - Create new subject
GET    /api/subjects           - Get all user subjects
GET    /api/subjects/:id       - Get specific subject
POST   /api/subjects/:id/topics - Add topic to subject
```

### Timetable Generation
```
POST   /api/subjects/:id/generate-timetable  - Generate AI timetable
GET    /api/subjects/:id/timetable           - Get generated timetable
```

### Analysis & Insights
```
GET    /api/subjects/:id/weak-topics         - Identify weak topics
POST   /api/subjects/:id/generate-notes      - Generate AI notes
POST   /api/subjects/:id/generate-questions  - Generate practice questions
GET    /api/subjects/:id/analytics           - Get progress analytics
```

### Study Tracking
```
POST   /api/subjects/:id/study-session       - Record study session
```

---

## 🎯 Features Implemented

### Phase 1: Foundation ✅
- User Authentication (JWT)
- Subject & Syllabus Management
- User Profile Management

### Phase 2: Smart Algorithms ✅
- Timetable Generation Algorithm
- Weak Topic Detection System
- Analytics & Progress Tracking

### Phase 3: AI Integration ✅
- AI Notes Generation (OpenAI)
- Practice Question Generation
- Study Recommendations

### Phase 4: Dashboard (In Progress)
- Visual Progress Charts
- Weekly/Monthly Analytics
- Weak Topic Insights
- Exam Readiness Score

### Phase 5: Advanced Features (Planned)
- Push Notifications
- Email Reminders
- Multi-device Sync
- AI Chatbot for Doubts
- Voice Study Tracking
- Rank Prediction

---

## 🔧 Configuration Guide

### MongoDB Setup
```javascript
// After installing MongoDB: Replace in-memory data with MongoDB
const mongoose = require('mongoose');

mongoose.connect(process.env.MONGODB_URI, {
    useNewUrlParser: true,
    useUnifiedTopology: true
});
```

### OpenAI API Setup
1. Get API key from https://openai.com/api/
2. Add to `.env`: `OPENAI_API_KEY=sk-...`
3. Notes generator will work automatically

### Email Notifications (Optional)
```javascript
// Add Nodemailer configuration for email reminders
const nodemailer = require('nodemailer');
```

---

## 📊 Database Schema

### User Collection
```javascript
{
    id, fullname, email, password,
    studyHoursPerDay, preferredNotification,
    createdAt, updatedAt
}
```

### Subject Collection
```javascript
{
    userId, subjectName, examDate,
    topics: [
        { topicName, difficulty, estimatedHours, 
          completed, weaknessScore, quizScore }
    ],
    totalTopics, completedTopics,
    totalEstimatedHours, completedHours
}
```

### Timetable Collection
```javascript
{
    userId, subjectId,
    schedule: [
        { date, topic, estimatedHours, 
          priority, type, completed }
    ]
}
```

### Analytics Collection
```javascript
{
    userId, date,
    dailyStudyHours, topicsCompletedToday,
    averageProductivity, weakTopics, strongTopics,
    examReadinessScore, streakDays
}
```

---

## 🧪 Testing

### Test Timetable Generation
```
curl -X POST http://localhost:5000/api/subjects/{id}/generate-timetable \
  -H "Authorization: Bearer {token}" \
  -H "Content-Type: application/json"
```

### Test AI Notes
```
curl -X POST http://localhost:5000/api/subjects/{id}/generate-notes \
  -H "Authorization: Bearer {token}" \
  -d '{"topicName":"Operating Systems","difficulty":"Hard"}'
```

---

## 📈 8-Week Development Timeline

| Week | Tasks | Status |
|------|-------|--------|
| 1 | Requirements & UI Design | ✅ |
| 2 | Auth System | ✅ |
| 3 | Syllabus Module | ✅ |
| 4 | Timetable Algorithm | ✅ |
| 5 | AI Notes Integration | ✅ |
| 6 | Analytics Dashboard | 🔄 |
| 7 | Testing & Bug Fixes | ⏳ |
| 8 | Deployment | ⏳ |

---

## 🌟 Advanced Features (Extra)

- 🤖 **AI Chatbot** - Doubt solving chatbot
- 🎤 **Voice Tracking** - Voice-based study sessions
- 📊 **Rank Prediction** - Exam rank prediction
- 👥 **Peer Comparison** - Compare with other learners
- 📱 **Mobile App** - React Native application
- 🔔 **Smart Notifications** - AI-powered reminder system

---

## 🤝 Contributing

1. Fork the repository
2. Create feature branch: `git checkout -b feature/AmazingFeature`
3. Commit changes: `git commit -m 'Add AmazingFeature'`
4. Push to branch: `git push origin feature/AmazingFeature`
5. Open Pull Request

---

## 📝 License

This project is licensed under the MIT License - see LICENSE file for details.

---

## 📞 Support & Documentation

For detailed documentation on each module, check the service files:
- **Timetable Algorithm**: `backend/services/TimetableGenerator.js`
- **Weak Topic Analysis**: `backend/services/WeakTopicAnalyzer.js`
- **AI Integration**: `backend/services/AINotesGenerator.js`
- **Analytics**: `backend/services/AnalyticsService.js`

---

**Built with ❤️ for smarter studying**
