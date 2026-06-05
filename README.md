# Convo Sphere - Unified AI-Powered Communication Hub

A modern web application that centralizes conversations from multiple communication platforms (Email, WhatsApp, Slack, Telegram) into a single intelligent dashboard with AI-powered automation.

## 🌟 Project Overview

**Convo Sphere** is a production-ready MVP that transforms customer communication management by:
- Unifying multiple communication channels into a single interface
- Leveraging AI for intelligent message analysis and automated responses
- Providing real-time conversation management with advanced filtering
- Offering a modern, responsive UI built with cutting-edge technologies

## 📊 Current Implementation Status

### ✅ Completed Features

#### Backend (FastAPI)
- **Authentication System** - Complete JWT-based auth with user registration, login, and profile management
- **Database Integration** - MongoDB with Motor async driver for all data persistence
- **API Endpoints** - Full REST API for conversations, messages, and user management
- **Conversation Management** - Create, filter, and retrieve conversations with metadata
- **Message Processing** - Message ingestion, retrieval, and agent response posting
- **Integrations Foundation** - API endpoints for connecting Telegram, Slack, and Gmail
- **Statistics Dashboard** - System stats and metrics endpoints

#### Frontend (React 19)
- **Authentication Pages** - Complete login/register interface with form validation
- **Main Application Layout** - Dashboard, Inbox, and Integrations pages
- **UI Components** - 30+ Shadcn/UI components with Tailwind CSS styling
- **Navigation** - React Router v7 with protected routes
- **Responsive Design** - Mobile-first design with glassmorphism effects

#### Infrastructure
- **Development Environment** - Hot reload for both frontend and backend
- **Database Schema** - Complete MongoDB collections for users, conversations, and messages
- **Security** - Password hashing with bcrypt, JWT tokens, CORS configuration

### 🚧 In Progress / Partially Implemented

#### AI Integration
- OpenAI API integration foundation exists but analysis functions need implementation
- Mock data structures for sentiment analysis, intent detection, and priority classification
- Auto-response generation framework ready for AI implementation

#### Multi-Channel Integration
- **Telegram** - Basic polling endpoint implemented
- **Gmail** - OAuth flow started, callback handling needed
- **Slack** - Connection endpoint ready, webhook handling needed
- **WhatsApp** - Configuration UI exists, API integration needed

### ❌ Not Yet Implemented

#### Real-time Features
- WebSocket connection for live message updates
- Server → Client message broadcasting
- Live conversation status updates

#### Advanced Features
- Full AI model integration with confidence scoring
- Automated response system with validation
- Advanced analytics and reporting
- Team collaboration with multiple agents

## 🛠️ Technology Stack

### Backend
- **Framework**: FastAPI (Python 3.11+)
- **Database**: MongoDB with Motor (async driver)
- **AI/NLP**: OpenAI GPT integration (ready for implementation)
- **Authentication**: JWT (JSON Web Tokens) with bcrypt
- **API Documentation**: Auto-generated OpenAPI/Swagger docs

### Frontend
- **Framework**: React 19 with modern hooks
- **Routing**: React Router v7
- **UI Components**: Shadcn/UI with Radix UI primitives (30+ components)
- **Styling**: Tailwind CSS with custom design system
- **State Management**: React Context API
- **Notifications**: Sonner (toast notifications)
- **Icons**: Lucide React
- **Forms**: React Hook Form with Zod validation
- **Charts**: Recharts for data visualization

### Development Tools
- **Package Manager**: Yarn (frontend), pip (backend)
- **Code Quality**: ESLint, Prettier, Black formatting
- **Testing**: Jest, React Testing Library (framework ready)
- **Hot Reload**: Vite (frontend), Uvicorn (backend)

## 📋 Prerequisites

- **Node.js** (v16+)
- **Python 3.11+**
- **MongoDB 5.0+** (local or MongoDB Atlas)
- **Yarn package manager**
- **API Keys** (for AI and channel integrations)

## 🚀 Quick Start

### 1. Environment Setup

#### Backend Environment (`backend/.env`)
```bash
# Database
MONGO_URL=mongodb://localhost:27017
DB_NAME=convo_sphere

# Authentication
JWT_SECRET=your-super-secret-jwt-key-here
JWT_ALGORITHM=HS256

# AI Integration
EMERGENT_LLM_KEY=your-openai-api-key-here

# CORS
CORS_ORIGINS=http://localhost:3000

# Channel Integrations (Optional)
GMAIL_CLIENT_ID=your-gmail-client-id
GMAIL_CLIENT_SECRET=your-gmail-client-secret
TELEGRAM_BOT_TOKEN=your-telegram-bot-token
SLACK_BOT_TOKEN=your-slack-bot-token
WHATSAPP_BUSINESS_API_KEY=your-whatsapp-api-key
```

#### Frontend Environment (`frontend/.env`)
```bash
VITE_BACKEND_URL=http://localhost:8000
VITE_API_TIMEOUT=30000
```

### 2. Installation & Setup

```bash
# Clone the repository
git clone <repository-url>
cd convo

# Backend Setup
cd backend
python -m venv venv
# Windows: venv\Scripts\activate
# Mac/Linux: source venv/bin/activate
pip install -r requirements.txt

# Frontend Setup
cd ../frontend
yarn install

# Database Setup
# Start MongoDB locally or configure MongoDB Atlas
# Update MONGO_URL in backend/.env if using Atlas
```

### 3. Running the Application

#### Option A: Development Mode
```bash
# Terminal 1 - Backend
cd backend
python server.py
# Runs on http://localhost:8000

# Terminal 2 - Frontend
cd frontend
yarn start
# Runs on http://localhost:3000
```

#### Option B: Production Mode (Docker)
```bash
# Build and run with Docker Compose
docker-compose up -d
```

### 4. Initial Data Setup (Optional)
```bash
# Seed sample data for testing
python scripts/seed_data.py
```

## 📊 Database Schema

### Collections Overview

#### Users Collection
```javascript
{
  id: String,           // Unique user identifier
  email: String,        // User email (unique)
  name: String,         // Display name (optional)
  role: String,         // User role (admin, agent)
  password: String,     // Hashed password
  created_at: String    // ISO timestamp
}
```

#### Conversations Collection
```javascript
{
  id: String,                    // Unique conversation ID
  customer_name: String,         // Customer display name
  customer_contact: String,      // Contact identifier
  channel: String,               // email, whatsapp, slack, telegram
  status: String,                // open, waiting, resolved
  priority: String,              // low, medium, high
  sentiment: String,             // positive, neutral, negative
  intent: String,                // question, complaint, request, etc.
  assigned_to: String,           // Agent ID (optional)
  last_message_at: String,       // ISO timestamp
  created_at: String,            // ISO timestamp
  unread_count: Number           // Unread messages count
}
```

#### Messages Collection
```javascript
{
  id: String,                    // Unique message ID
  conversation_id: String,       // Parent conversation ID
  sender_type: String,           // customer, agent, ai
  sender_name: String,           // Sender display name
  content: String,               // Message content
  channel: String,               // Message channel
  timestamp: String,             // ISO timestamp
  metadata: Object               // Additional message data
}
```

## 🔌 API Endpoints Reference

### Authentication Endpoints
```
POST   /api/auth/register        # Register new user
POST   /api/auth/login           # User login
GET    /api/auth/me              # Get current user info
POST   /api/auth/logout          # Logout user
GET    /api/auth/debug/users     # Debug: List all users
```

### Conversation Management
```
POST   /api/conversations                    # Create new conversation
POST   /api/conversations/filter             # Filter conversations
GET    /api/conversations/{id}               # Get conversation details
GET    /api/conversations/{id}/messages      # Get conversation messages
POST   /api/conversations/{id}/respond       # Send agent response
```

### Message Processing
```
POST   /api/messages/ingest                  # Ingest new message
```

### Integration Endpoints
```
POST   /api/integrations/telegram/connect    # Connect Telegram bot
POST   /api/integrations/slack/connect       # Connect Slack workspace
GET    /api/integrations/gmail/authorize     # Start Gmail OAuth
POST   /api/integrations/gmail/callback      # Handle Gmail OAuth callback
GET    /api/integrations/user                # Get user integrations
```

### System Endpoints
```
GET    /api/stats                            # Get dashboard statistics
GET    /api/telegram/poll                    # Telegram message polling
WS     /ws                                   # WebSocket endpoint (future)
```

## 🎨 Design System

### Typography
- **Headings**: Manrope (Bold/ExtraBold)
- **Body Text**: Inter (Regular/Medium)
- **Code**: JetBrains Mono

### Color Palette
- **Primary**: Electric Indigo (#4338ca)
- **Background**: White (#ffffff)
- **Foreground**: Slate 900 (#0f172a)
- **Muted**: Slate 100 (#f8fafc)
- **Border**: Slate 200 (#e2e8f0)
- **Success**: Emerald (#10b981)
- **Warning**: Amber (#f59e0b)
- **Error**: Red (#ef4444)

### UI Components
- **Glassmorphism**: Subtle blur effects for headers
- **Card Layout**: Clean card-based layouts with hover effects
- **Badge System**: Status indicators for conversations
- **3-Pane Inbox**: Optimized layout for conversation management

## 🧪 Testing

### Manual Testing Checklist

#### Authentication ✅
- [x] User registration with email validation
- [x] User login with JWT token generation
- [x] Password hashing and verification
- [x] Protected route access control

#### Core Features ✅
- [x] Dashboard page loads with user context
- [x] Inbox page structure with 3-pane layout
- [x] Navigation between pages
- [x] Toast notifications for user feedback

#### API Endpoints ✅
- [x] All authentication endpoints
- [x] Conversation CRUD operations
- [x] Message ingestion and retrieval
- [x] Statistics endpoint

#### Integration Framework ⚠️
- [ ] Gmail OAuth flow completion
- [ ] Telegram bot connection testing
- [ ] Slack workspace connection
- [ ] WhatsApp Business API setup

#### AI Features ❌
- [ ] Message sentiment analysis
- [ ] Intent detection
- [ ] Priority classification
- [ ] Auto-response generation

### Test User Account
For testing purposes, you can use:
- **Email**: `test@example.com`
- **Password**: `password123`

Or create a new account through the registration page.

## 📱 User Interface

### Page Structure

#### 1. Login/Register Page
- Split-screen design with brand imagery
- Toggle between login and registration modes
- Form validation with real-time feedback
- Social login options (future enhancement)

#### 2. Dashboard Page
- Key metrics overview (unread count, response time)
- Conversation volume charts
- Agent performance metrics
- Quick action buttons

#### 3. Inbox Page (3-Pane Layout)
- **Left Pane**: Channel filters and search
- **Middle Pane**: Conversation list with status indicators
- **Right Pane**: Message history and composition area

#### 4. Integrations Page
- Connected services overview
- Connection status indicators
- Setup wizards for each channel

## 🔒 Security Features

- **Password Security**: bcrypt hashing with salt rounds
- **Authentication**: JWT tokens with configurable expiration
- **CORS Protection**: Configurable allowed origins
- **Input Validation**: Pydantic models for API validation
- **SQL Injection Prevention**: MongoDB ORM protection
- **XSS Protection**: React's built-in XSS mitigation

## 🚢 Deployment

### Development Environment
```bash
# Backend
cd backend
uvicorn server:app --host 0.0.0.0 --port 8000 --reload

# Frontend
cd frontend
yarn start
```

### Production Deployment
```bash
# Build frontend
cd frontend
yarn build

# Run backend with production server
cd backend
uvicorn server:app --host 0.0.0.0 --port 8000
```

### Docker Deployment
```dockerfile
# Dockerfile example (to be created)
FROM node:18-alpine as frontend-build
# Frontend build steps...

FROM python:3.11-slim as backend
# Backend setup...
```

## 📝 Future Roadmap

### Phase 1: AI Integration (Next Sprint)
- [ ] Complete OpenAI API integration
- [ ] Implement sentiment analysis pipeline
- [ ] Add intent detection algorithms
- [ ] Build auto-response generation system
- [ ] Add confidence scoring for AI predictions

### Phase 2: Channel Integration (Following Sprint)
- [ ] Complete Gmail OAuth and email polling
- [ ] Implement WhatsApp Business API
- [ ] Build Slack real-time integration
- [ ] Enhance Telegram bot functionality
- [ ] Add message synchronization

### Phase 3: Real-time Features
- [ ] WebSocket implementation for live updates
- [ ] Real-time message streaming
- [ ] Live typing indicators
- [ ] Online presence status
- [ ] Push notifications

### Phase 4: Advanced Features
- [ ] Multi-agent collaboration
- [ ] Conversation assignment system
- [ ] Advanced analytics dashboard
- [ ] Custom response templates
- [ ] Conversation tagging system
- [ ] Full-text search functionality

### Phase 5: Mobile & Scaling
- [ ] React Native mobile app
- [ ] Advanced user roles and permissions
- [ ] API rate limiting
- [ ] Caching layer implementation
- [ ] Performance optimization

## 🐛 Known Issues & Troubleshooting

### Current Issues
- WebSocket connection errors in console (expected - not yet implemented)
- Integration endpoints return mock data (needs actual API connections)
- AI analysis endpoints return placeholder responses

### Common Solutions

#### Port Conflicts
```bash
# Kill processes on ports 8000 and 3000
netstat -tulpn | grep :8000
kill -9 <PID>
```

#### Database Connection Issues
```bash
# Check MongoDB connection
mongosh
> use convo_sphere
> db.users.find()
```

#### CORS Errors
- Ensure `VITE_BACKEND_URL` in frontend `.env` matches backend URL
- Update `CORS_ORIGINS` in backend `.env` to include frontend URL

#### JWT Token Issues
- Clear browser localStorage
- Verify `JWT_SECRET` is consistent across restarts
- Check token expiration settings

## 🤝 Contributing Guidelines

### Development Workflow
1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make changes with proper testing
4. Update documentation as needed
5. Submit a pull request

### Code Standards
- **Backend**: Follow PEP 8, use Black formatter
- **Frontend**: Use ESLint + Prettier configuration
- **Commits**: Use conventional commit messages
- **Testing**: Write tests for new features

### Project Structure
```
convo/
├── backend/                 # FastAPI application
│   ├── server.py          # Main application file
│   ├── requirements.txt   # Python dependencies
│   └── .env              # Environment variables
├── frontend/              # React application
│   ├── src/
│   │   ├── components/   # Reusable UI components
│   │   ├── pages/       # Page components
│   │   ├── hooks/       # Custom React hooks
│   │   └── lib/         # Utility functions
│   ├── package.json     # Node dependencies
│   └── .env            # Frontend environment
├── scripts/             # Utility scripts
├── tests/              # Test files
└── docs/              # Documentation
```

## 📄 License

Proprietary - Convo Sphere

## 📞 Support & Contact

For technical support, feature requests, or bug reports:
- Create an issue in the project repository
- Contact the development team
- Check the troubleshooting section above

---

**Last Updated**: April 14, 2026  
**Version**: 1.0.0-alpha  
**Status**: Development - Core Features Complete, AI & Integration Pending

**Built with Modern Technologies** - React 19, FastAPI, MongoDB, Tailwind CSS, and AI-powered automation capabilities.
