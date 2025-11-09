# EnterVU: Detailed Project Description

## Table of Contents
1. [Project Overview](#project-overview)
2. [System Architecture](#system-architecture)
3. [Technology Stack](#technology-stack)
4. [Core Features](#core-features)
5. [Database Schema](#database-schema)
6. [API Architecture](#api-architecture)
7. [Frontend Architecture](#frontend-architecture)
8. [AI Integration](#ai-integration)
9. [Authentication & Security](#authentication--security)
10. [Deployment & Infrastructure](#deployment--infrastructure)
11. [User Workflow](#user-workflow)
12. [Development Setup](#development-setup)
13. [Testing Strategy](#testing-strategy)
14. [Future Enhancements](#future-enhancements)

---

## Project Overview

**EnterVU** is an advanced AI-powered interview preparation and evaluation system designed to help job candidates practice and improve their interview skills in a realistic, interactive environment. The platform leverages cutting-edge artificial intelligence technology from Google's Gemini AI to simulate authentic interview experiences.

### Purpose & Goals

The primary objectives of EnterVU are to:

- **Democratize Interview Preparation**: Provide accessible, high-quality interview practice for job seekers regardless of their location or resources
- **Personalized Learning**: Tailor interview questions and feedback based on individual CV profiles, target job roles, and skill levels
- **Realistic Simulation**: Create an authentic interview environment through both text-based and voice-based interaction modes
- **Actionable Feedback**: Deliver comprehensive evaluation reports with specific strengths, weaknesses, and improvement recommendations
- **Skill Assessment**: Evaluate technical competencies, behavioral responses, and communication abilities

### Key Differentiators

1. **AI-Driven CV Parsing**: Automatically extracts and structures information from uploaded CVs using Google's Generative AI
2. **Dual Interview Modes**: Supports both traditional text-based chat interviews and innovative real-time voice conversations
3. **Dynamic Question Generation**: Creates unique, contextually relevant questions for each interview session
4. **Comprehensive Reporting**: Provides detailed analysis with scoring, transcripts, and actionable feedback
5. **Email Integration**: Automatically delivers interview reports via email using Gmail API

---

## System Architecture

EnterVU follows a modern microservices architecture with three distinct services:

### Architecture Components

```
┌─────────────────────────────────────────────────────────────┐
│                     Frontend (React + Vite)                 │
│                         Port: 5173                          │
└──────────────────┬──────────────────┬───────────────────────┘
                   │                  │
                   ▼                  ▼
    ┌──────────────────────┐  ┌──────────────────────┐
    │   Backend API        │  │   Live Agent API     │
    │   (FastAPI)          │  │   (FastAPI + ADK)    │
    │   Port: 5000         │  │   Port: 8000         │
    └──────────┬───────────┘  └──────────┬───────────┘
               │                         │
               ▼                         ▼
    ┌──────────────────────┐  ┌──────────────────────┐
    │   SQLite Database    │  │   Google Gemini AI   │
    │   (SQLAlchemy)       │  │   (via ADK)          │
    └──────────────────────┘  └──────────────────────┘
```

### Service Breakdown

#### 1. Backend API Service (Port 5000)
- **Responsibility**: Core REST API for the application
- **Functions**:
  - User authentication and session management
  - CV upload, storage, and parsing
  - Interview creation and management
  - Question and answer handling
  - Report generation and storage
  - Email notification dispatch
- **Database**: SQLite with SQLAlchemy ORM
- **Framework**: FastAPI with Pydantic validation

#### 2. Live Agent Service (Port 8000)
- **Responsibility**: Real-time voice interview processing
- **Functions**:
  - Server-Sent Events (SSE) for live streaming
  - Real-time audio processing (PCM format)
  - Voice-to-voice AI conversation
  - Google ADK integration for live sessions
- **Technology**: FastAPI + Google Agent Development Kit

#### 3. Frontend Service (Port 5173)
- **Responsibility**: User interface and client-side logic
- **Functions**:
  - User registration and login
  - CV management interface
  - Interview configuration
  - Real-time interview interaction
  - Report visualization
  - API documentation browser
- **Technology**: React 18 + Vite + Tailwind CSS

---

## Technology Stack

### Backend Technologies

#### Core Framework
- **FastAPI 0.116.1**: High-performance async web framework
  - Built-in OpenAPI/Swagger documentation
  - Automatic request validation via Pydantic
  - WebSocket and SSE support
  - Async/await support for high concurrency

#### Database & ORM
- **SQLAlchemy 2.0.43**: Python SQL toolkit and ORM
  - Declarative base for model definitions
  - Relationship mapping
  - Query optimization
- **SQLite**: Lightweight, file-based relational database
- **Alembic 1.16.5**: Database migration tool

#### AI & Machine Learning
- **Google ADK (Agent Development Kit) 1.15.1**: Google's framework for building AI agents
- **LangChain 0.3.27**: Framework for developing LLM-powered applications
- **LangChain Community 0.3.29**: Community integrations

#### Data Processing
- **PyPDF2 3.0.1**: PDF parsing and text extraction
- **Pydantic 2.11.9**: Data validation using Python type annotations
- **python-multipart 0.0.20**: Multipart form data parsing

#### External APIs
- **google-api-python-client 2.184.0**: Google API client library
- **google-auth-oauthlib 1.2.2**: OAuth 2.0 authentication
- **google-auth-httplib2 0.2.0**: HTTP library for Google APIs

#### Testing
- **pytest 8.4.2**: Testing framework
- **pytest-asyncio 1.2.0**: Async test support
- **pytest-dependency 0.6.0**: Test dependency management
- **httpx 0.28.1**: Async HTTP client for testing

#### Utilities
- **uvicorn 0.35.0**: ASGI server
- **python-dotenv 1.1.1**: Environment variable management
- **aiofiles 24.1.0**: Async file I/O

### Frontend Technologies

#### Core Framework
- **React 18.3.1**: Modern UI library
  - Functional components with Hooks
  - Context API for state management
  - Virtual DOM for performance

#### Build Tools
- **Vite 5.3.1**: Next-generation frontend build tool
  - Lightning-fast HMR (Hot Module Replacement)
  - Optimized production builds
  - ES modules support

#### Routing
- **React Router DOM 6.24.1**: Client-side routing
  - Declarative routing
  - Nested routes
  - Protected routes

#### Styling
- **Tailwind CSS 3.4.4**: Utility-first CSS framework
  - Responsive design utilities
  - Custom configuration
  - JIT (Just-In-Time) compilation
- **PostCSS 8.4.39**: CSS transformation tool
- **Autoprefixer 10.4.19**: CSS vendor prefixing

#### HTTP Client
- **Axios 1.7.2**: Promise-based HTTP client
  - Request/response interceptors
  - Automatic JSON transformation
  - Error handling

#### UI Components
- **Lucide React 0.408.0**: Icon library
  - Modern SVG icons
  - Tree-shakeable
  - Customizable

#### Code Quality
- **ESLint 8.57.0**: JavaScript linter
  - React-specific rules
  - Custom configurations
  - Auto-fixing capabilities

#### Audio Processing
- **Web Audio API**: Browser-native audio processing
- **AudioWorklets**: Real-time audio processing in separate threads
- **PCM (Pulse Code Modulation)**: Uncompressed audio format for streaming

### Infrastructure

#### Containerization
- **Docker**: Container platform
- **Docker Compose 3.8**: Multi-container orchestration
  - Service networking
  - Volume management
  - Environment configuration

#### Web Server
- **Nginx**: Reverse proxy and static file server for production frontend

---

## Core Features

### 1. User Authentication System

#### Registration
- Email-based account creation
- Password validation and hashing
- Automatic account activation
- User profile initialization

#### Login
- Secure credential verification
- Session token generation
- JWT-based authentication
- Remember me functionality

#### Security
- Password encryption using industry-standard algorithms
- Session management with secure tokens
- Protected API endpoints
- CORS (Cross-Origin Resource Sharing) configuration

### 2. CV Management

#### Upload Functionality
- Multiple CV support per user
- PDF file format support
- File size validation
- Unique file naming and storage

#### AI-Powered Parsing
- Automatic information extraction using Google's Generative AI
- Structured data output (JSON format)
- Field extraction:
  - Personal information (name, contact details)
  - Work experience (companies, positions, dates, responsibilities)
  - Education (degrees, institutions, graduation dates)
  - Skills (technical, soft skills, languages)
  - Certifications and achievements
  - Projects and publications

#### Storage & Retrieval
- Persistent file storage in backend
- CV metadata in database
- Quick access and deletion
- File preview capabilities

### 3. Interview System

#### Interview Configuration
- **CV Selection**: Choose from uploaded CVs
- **Job Title**: Specify target position
- **Job Description**: Optional detailed job requirements
- **Skills Focus**: Highlight specific skills to evaluate
- **Difficulty Level**: Select from Easy, Medium, Hard, Expert
- **Mode Selection**: Text-based or Voice-based interview

#### Text-Based Interview Mode
- Chat-style interface
- Real-time question delivery
- Text input for answers
- Question progression control
- Ability to review previous questions
- Session persistence

#### Voice-Based Interview Mode
- Real-time voice-to-voice conversation
- Automatic speech recognition (ASR)
- Text-to-speech (TTS) synthesis
- Natural conversation flow
- Low-latency audio streaming
- Session recording

#### Question Generation
- AI-driven question creation
- Context-aware questions based on:
  - CV content
  - Job requirements
  - Selected skills
  - Difficulty level
- Question types:
  - Technical questions
  - Behavioral questions (STAR method)
  - Situational questions
  - Problem-solving scenarios
- Dynamic follow-up questions

### 4. Interview Evaluation & Reporting

#### Automated Evaluation
- AI-powered answer analysis
- Multi-dimensional scoring:
  - Technical accuracy
  - Communication clarity
  - Problem-solving approach
  - Behavioral indicators
  - Cultural fit
- Overall score calculation (0-100 scale)
- Pass/Fail decision

#### Report Generation
- Comprehensive PDF report creation
- Report sections:
  - **Executive Summary**: Overall score and decision
  - **Strengths**: Areas of excellence
  - **Weaknesses**: Areas for improvement
  - **Detailed Feedback**: Question-by-question analysis
  - **Full Transcript**: Complete conversation record
  - **Recommendations**: Actionable improvement suggestions
- Persistent storage in backend
- Download functionality

#### Email Delivery
- Automatic report email dispatch
- Gmail API integration
- Professional email formatting
- Attachment support
- Delivery confirmation

### 5. Dashboard & History

#### User Dashboard
- Interview history overview
- CV library management
- Quick access to reports
- Statistics and analytics
- Recent activity tracking

#### Interview History
- List of all past interviews
- Interview metadata:
  - Date and time
  - Job title
  - Score achieved
  - Interview mode
  - Duration
- Quick report access
- Search and filter capabilities

### 6. API Documentation

#### Interactive Documentation
- Embedded API explorer in frontend
- Endpoint categorization
- Request/response examples
- Authentication requirements
- Try-it-out functionality

#### Postman Collection
- Pre-configured API collection
- Environment variables
- Sample requests
- Testing workflows

---

## Database Schema

### Entity-Relationship Model

```
User (1) ──────< (M) CV
  │
  └──────< (M) Interview
                  │
                  ├──────< (M) Question
                  │           │
                  │           └──────< (M) QuestionTopicAssociation
                  │                           │
                  │                           └──────> (1) Topic
                  ├──────< (M) Answer
                  │
                  └──────> (1) Report
```

### Database Tables

#### User Table
```sql
- id: INTEGER (Primary Key)
- username: VARCHAR(255) (Unique, Not Null)
- email: VARCHAR(255) (Unique, Not Null)
- password: VARCHAR(255) (Hashed, Not Null)
- created_at: DATETIME
- updated_at: DATETIME
```

#### CV Table
```sql
- id: INTEGER (Primary Key)
- user_id: INTEGER (Foreign Key -> User.id, Cascade Delete)
- file_name: VARCHAR(255)
- file_path: VARCHAR(500)
- parsed_data: JSON (Structured CV information)
- uploaded_at: DATETIME
- updated_at: DATETIME
```

#### Interview Table
```sql
- id: INTEGER (Primary Key)
- user_id: INTEGER (Foreign Key -> User.id, Cascade Delete)
- cv_id: INTEGER (Foreign Key -> CV.id)
- job_title: VARCHAR(255)
- job_description: TEXT
- difficulty_level: VARCHAR(50)
- mode: VARCHAR(50) (text/voice)
- status: VARCHAR(50) (in_progress/completed/abandoned)
- created_at: DATETIME
- completed_at: DATETIME
- updated_at: DATETIME
```

#### Question Table
```sql
- id: INTEGER (Primary Key)
- interview_id: INTEGER (Foreign Key -> Interview.id, Cascade Delete)
- content: TEXT (Question text)
- type: VARCHAR(50) (technical/behavioral/situational)
- order: INTEGER (Question sequence)
- created_at: DATETIME
```

#### Answer Table
```sql
- id: INTEGER (Primary Key)
- question_id: INTEGER (Foreign Key -> Question.id, Cascade Delete)
- content: TEXT (User's answer)
- created_at: DATETIME
```

#### Topic Table
```sql
- id: INTEGER (Primary Key)
- name: VARCHAR(255) (Skill/topic name)
- created_at: DATETIME
```

#### QuestionTopicAssociation Table
```sql
- question_id: INTEGER (Foreign Key -> Question.id, Cascade Delete)
- topic_id: INTEGER (Foreign Key -> Topic.id, Cascade Delete)
- Primary Key: (question_id, topic_id)
```

#### Report Table
```sql
- id: INTEGER (Primary Key)
- interview_id: INTEGER (Foreign Key -> Interview.id, Cascade Delete)
- final_score: FLOAT (0-100)
- decision: VARCHAR(50) (Pass/Fail)
- strengths: TEXT (JSON array)
- weaknesses: TEXT (JSON array)
- feedback: TEXT
- file_path: VARCHAR(500) (PDF report path)
- created_at: DATETIME
- updated_at: DATETIME
```

### Database Features

- **Cascading Deletes**: Automatic cleanup of related records
- **Indexes**: Optimized queries on frequently accessed columns
- **JSON Storage**: Flexible storage for structured data (CV parsing, report details)
- **Timestamps**: Audit trail with created_at and updated_at fields
- **Referential Integrity**: Foreign key constraints maintain data consistency

---

## API Architecture

### RESTful API Design

EnterVU follows REST principles with a versioned API (V2).

#### API Endpoints Structure

##### Authentication Endpoints
```
POST   /api/v2/auth/register    - User registration
POST   /api/v2/auth/login       - User login
POST   /api/v2/auth/logout      - User logout
GET    /api/v2/auth/me          - Get current user
```

##### CV Endpoints
```
GET    /api/v2/cvs               - List user's CVs
POST   /api/v2/cvs               - Upload new CV
GET    /api/v2/cvs/{cv_id}       - Get CV details
DELETE /api/v2/cvs/{cv_id}       - Delete CV
POST   /api/v2/cvs/{cv_id}/parse - Parse CV with AI
```

##### Interview Endpoints
```
GET    /api/v2/interviews                    - List user's interviews
POST   /api/v2/interviews                    - Create new interview
GET    /api/v2/interviews/{interview_id}     - Get interview details
PUT    /api/v2/interviews/{interview_id}     - Update interview
DELETE /api/v2/interviews/{interview_id}     - Delete interview
POST   /api/v2/interviews/{interview_id}/start - Start interview session
POST   /api/v2/interviews/{interview_id}/finish - Complete interview
```

##### Question Endpoints
```
GET    /api/v2/interviews/{interview_id}/questions           - List questions
POST   /api/v2/interviews/{interview_id}/questions           - Add question
GET    /api/v2/interviews/{interview_id}/questions/{q_id}    - Get question
```

##### Answer Endpoints
```
POST   /api/v2/questions/{question_id}/answers               - Submit answer
GET    /api/v2/questions/{question_id}/answers               - Get answers
```

##### Report Endpoints
```
GET    /api/v2/interviews/{interview_id}/report              - Get report
POST   /api/v2/interviews/{interview_id}/report/email        - Email report
GET    /api/v2/reports/{report_id}/download                  - Download PDF
```

##### Live Interview Endpoints (Port 8000)
```
GET    /live/interview/{session_id}          - SSE connection for live interview
POST   /live/audio                           - Audio stream endpoint
```

### Request/Response Format

#### Standard Response Structure
```json
{
  "success": true,
  "data": { ... },
  "message": "Operation successful",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

#### Error Response Structure
```json
{
  "success": false,
  "error": {
    "code": "INVALID_INPUT",
    "message": "Validation failed",
    "details": { ... }
  },
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### API Features

- **Authentication**: JWT bearer tokens
- **Validation**: Pydantic schemas for request/response validation
- **Error Handling**: Consistent error responses with appropriate HTTP status codes
- **Rate Limiting**: Configurable request throttling
- **CORS**: Cross-origin support for frontend
- **Documentation**: Auto-generated OpenAPI/Swagger docs

---

## Frontend Architecture

### Component Structure

```
src/
├── api/
│   └── apiClient.js              # Centralized API client
├── components/
│   ├── dashboard/
│   │   ├── CVList.jsx            # CV management component
│   │   └── InterviewHistoryList.jsx
│   ├── report/
│   │   ├── ScoreSummary.jsx      # Score display
│   │   ├── FeedbackCard.jsx      # Feedback sections
│   │   └── Transcript.jsx        # Conversation transcript
│   └── docs/
│       └── CodeBlock.jsx         # API docs code display
├── pages/
│   ├── LoginPage.jsx
│   ├── RegisterPage.jsx
│   ├── DashboardPage.jsx
│   ├── NewInterviewPage.jsx
│   ├── LiveInterviewPage.jsx     # Text interview
│   ├── LiveInterviewPageVoice.jsx # Voice interview
│   ├── InterviewReportPage.jsx
│   ├── ApiDocsPage.jsx
│   └── NotFoundPage.jsx
├── utils/
│   ├── audioUtils.js             # Audio processing utilities
│   └── audioWorklets/
│       ├── pcm-recorder-processor.js
│       └── pcm-player-processor.js
└── App.jsx                       # Main application component
```

### State Management

- **React Context**: Global state for authentication
- **Component State**: Local UI state with useState
- **React Router**: Navigation state management

### Routing

```javascript
- /login                  → LoginPage
- /register               → RegisterPage
- /dashboard              → DashboardPage (Protected)
- /new-interview          → NewInterviewPage (Protected)
- /interview/:id          → LiveInterviewPage (Protected)
- /interview/:id/voice    → LiveInterviewPageVoice (Protected)
- /report/:id             → InterviewReportPage (Protected)
- /docs                   → ApiDocsPage
- /*                      → NotFoundPage
```

### Audio Processing Architecture

#### Web Audio API Integration
- **AudioContext**: Main audio processing context
- **AudioWorklets**: Low-latency audio processing
- **MediaStream**: Microphone access

#### PCM Audio Streaming
- Real-time PCM encoding/decoding
- Configurable sample rate (16kHz default)
- Mono channel processing
- Efficient buffer management

---

## AI Integration

### Google Gemini AI

#### CV Parsing
- **Model**: Gemini 1.5 Pro
- **Task**: Information extraction from PDF text
- **Output**: Structured JSON with CV fields
- **Prompt Engineering**: Custom prompts for accurate extraction

#### Question Generation
- **Model**: Gemini 1.5 Pro
- **Input**: CV data, job description, difficulty level
- **Output**: Array of contextual questions
- **Diversity**: Ensures variety in question types

#### Answer Evaluation
- **Model**: Gemini 1.5 Pro
- **Input**: Question, answer, CV context
- **Output**: Score, feedback, strengths, weaknesses
- **Criteria**: Technical accuracy, communication, problem-solving

### Google Agent Development Kit (ADK)

#### Live Voice Agent
- Real-time conversation management
- Speech recognition and synthesis
- Context maintenance across turns
- Natural language understanding
- Adaptive responses based on user input

#### Streaming Architecture
- Server-Sent Events (SSE) for one-way streaming
- WebSocket alternative for bidirectional communication
- Low-latency audio transmission
- Automatic reconnection handling

---

## Authentication & Security

### Authentication Flow

1. **Registration**:
   - User submits credentials
   - Password hashed with secure algorithm
   - User record created in database
   - Auto-login with token generation

2. **Login**:
   - Credentials validated
   - JWT token generated with user claims
   - Token stored in browser (localStorage)
   - Token included in subsequent requests

3. **Authorization**:
   - Token validation on protected endpoints
   - User identity extraction from token
   - Permission checks for resource access

### Security Measures

- **Password Hashing**: Industry-standard hashing algorithms
- **JWT Tokens**: Secure token-based authentication
- **HTTPS**: Encrypted communication (production)
- **Input Validation**: Pydantic schema validation
- **SQL Injection Prevention**: SQLAlchemy ORM parameterization
- **XSS Protection**: React automatic escaping
- **CORS**: Configured allowed origins
- **File Upload Validation**: File type and size restrictions

---

## Deployment & Infrastructure

### Docker Containerization

#### Benefits
- Consistent environment across development and production
- Simplified dependency management
- Easy scaling and orchestration
- Isolated service containers

#### Container Configuration

**Backend API Container**:
- Python 3.11 base image
- Uvicorn ASGI server
- Port 5000 exposed
- Volume mounts for data persistence

**Live Agent Container**:
- Same base image as API
- Separate service instance
- Port 8000 exposed
- Shared environment configuration

**Frontend Container**:
- Node.js build stage
- Nginx production server
- Port 80 (mapped to 5173)
- Optimized static file serving

### Docker Compose Orchestration

- **Service Dependencies**: Frontend depends on both backends
- **Networking**: Automatic service discovery
- **Volume Management**: Persistent data storage
- **Environment Variables**: Centralized configuration

### Production Considerations

- **Reverse Proxy**: Nginx for request routing
- **SSL/TLS**: Certificate management for HTTPS
- **Monitoring**: Application and container monitoring
- **Logging**: Centralized log aggregation
- **Backup**: Database and file backup strategies
- **Scaling**: Horizontal scaling with load balancing

---

## User Workflow

### Complete Interview Journey

#### 1. Account Setup (5 minutes)
- Navigate to EnterVU application
- Click "Register" and provide email, username, password
- Automatic login after registration
- Redirected to dashboard

#### 2. CV Upload & Parsing (2-3 minutes)
- Click "Upload CV" on dashboard
- Select PDF file from computer
- System uploads and stores CV
- Click "Parse with AI" button
- AI extracts structured information
- Review parsed data for accuracy

#### 3. Interview Configuration (2 minutes)
- Click "New Interview" button
- Select CV from dropdown
- Enter target job title
- (Optional) Add detailed job description
- (Optional) Specify skills to focus on
- Choose difficulty level (Easy/Medium/Hard/Expert)
- Select interview mode (Text/Voice)
- Click "Start Interview"

#### 4A. Text-Based Interview (15-30 minutes)
- System generates opening question
- User types answer in text box
- Click "Submit Answer"
- System provides next question
- Continue until all questions answered
- Click "Finish Interview"

#### 4B. Voice-Based Interview (15-30 minutes)
- Grant microphone permissions
- Click "Start Voice Interview"
- AI interviewer asks question verbally
- User responds via microphone
- Natural conversation flow
- AI provides follow-up questions
- Click "End Interview" when complete

#### 5. Report Generation (1-2 minutes)
- System evaluates all answers
- AI generates comprehensive feedback
- Report created with:
  - Overall score
  - Pass/Fail decision
  - Strengths and weaknesses
  - Detailed feedback
  - Full transcript
- Report saved to dashboard

#### 6. Report Review & Email (5-10 minutes)
- Receive email notification
- Open report from dashboard or email
- Review overall score and decision
- Read strengths and weaknesses
- Study detailed feedback
- Review full transcript
- Download PDF for offline access
- Identify areas for improvement

#### 7. Iteration & Improvement (Ongoing)
- Upload updated CV with new skills
- Start new interview with different job role
- Increase difficulty level as skills improve
- Compare scores across interviews
- Track progress over time

---

## Development Setup

### Prerequisites

- **Docker Desktop**: Latest version with Docker Compose
- **Google API Key**: Gemini API access
- **Google Cloud Project**: Gmail API credentials
- **Git**: Version control

### Local Development Setup

#### 1. Clone Repository
```bash
git clone https://github.com/bilel-amri0/EnterVU-main.git
cd EnterVU-main
```

#### 2. Environment Configuration

**Backend Main API**:
```bash
cp backend/app/.env.example backend/app/.env
```

**Google ADK**:
```bash
cp backend/app/integrations/google_adk/.env.example backend/app/integrations/google_adk/.env
# Edit and add: GOOGLE_API_KEY="your_key_here"
```

#### 3. Google Credentials
- Download `credentials.json` from Google Cloud Console
- Place in: `backend/app/assets/creds/credentials.json`

#### 4. Data Directory Setup
```bash
mkdir -p backend/data
chmod -R 777 backend/data
```

#### 5. Build and Run
```bash
docker compose up --build -d
```

#### 6. Gmail Authentication (First Time)
- Complete first interview
- Check backend logs: `docker compose logs -f entervu-api`
- Copy authentication URL from logs
- Authorize in browser
- Token saved automatically

#### 7. Access Application
- Frontend: http://localhost:5173
- Backend API: http://localhost:5000
- Live Agent: http://localhost:8000
- API Docs: http://localhost:5000/docs

### Development Without Docker

#### Backend
```bash
cd backend/app
pip install -r requirements.txt
uvicorn main:app --reload --port 5000
```

#### Frontend
```bash
cd frontend
npm install
npm run dev
```

### Testing

#### Backend Tests
```bash
cd backend/app
pytest
pytest --cov  # With coverage
```

#### Frontend Linting
```bash
cd frontend
npm run lint
```

---

## Testing Strategy

### Backend Testing

#### Unit Tests
- Service layer tests
- Controller tests
- Model validation tests
- Utility function tests

#### Integration Tests
- API endpoint tests
- Database operation tests
- External API integration tests

#### Test Configuration
- **Framework**: pytest
- **Async Support**: pytest-asyncio
- **Dependencies**: pytest-dependency
- **HTTP Client**: httpx for API testing

### Frontend Testing

#### Code Quality
- **ESLint**: Code style and best practices
- **React Rules**: React-specific linting
- **Accessibility**: a11y checks

### Testing Best Practices

- Isolated test environments
- Mock external dependencies
- Comprehensive test coverage
- Continuous integration ready
- Automated test runs

---

## Future Enhancements

### Planned Features

#### 1. Advanced Analytics
- Interview performance trends
- Skill progression tracking
- Comparative analytics across interviews
- Industry benchmarking
- Personalized learning paths

#### 2. Multi-Language Support
- Internationalization (i18n)
- Multiple language interviews
- Localized feedback and reports
- Language proficiency assessment

#### 3. Interview Scheduling
- Calendar integration
- Scheduled practice sessions
- Reminder notifications
- Progress milestones

#### 4. Collaborative Features
- Peer review system
- Mentor feedback integration
- Interview sharing
- Community best practices

#### 5. Enhanced AI Capabilities
- Multi-modal AI (video analysis)
- Body language assessment
- Sentiment analysis
- Real-time coaching suggestions
- Adaptive difficulty based on performance

#### 6. Industry-Specific Templates
- Pre-configured interview templates by industry
- Role-specific question banks
- Company-specific preparation
- Technical assessment modules

#### 7. Mobile Application
- Native iOS app
- Native Android app
- Responsive web app improvements
- Offline practice mode

#### 8. Advanced Reporting
- Video recording playback
- Detailed analytics dashboard
- Exportable reports (multiple formats)
- Custom report templates
- Performance comparison tools

#### 9. Integration Ecosystem
- LinkedIn integration
- Job board connections
- ATS (Applicant Tracking System) integration
- Learning management systems
- HR platforms

#### 10. Gamification
- Achievement badges
- Leaderboards
- Skill challenges
- Progress rewards
- Certification programs

### Technical Improvements

- **Performance Optimization**:
  - Caching layer (Redis)
  - CDN for static assets
  - Database query optimization
  - Lazy loading and code splitting

- **Scalability**:
  - Kubernetes deployment
  - Microservices expansion
  - Load balancing
  - Auto-scaling configuration

- **Monitoring & Observability**:
  - Application performance monitoring (APM)
  - Error tracking (Sentry)
  - User analytics
  - Health checks and alerts

- **Security Enhancements**:
  - Two-factor authentication (2FA)
  - Single Sign-On (SSO)
  - Advanced encryption
  - Security audit logging
  - Penetration testing

---

## Conclusion

EnterVU represents a comprehensive, AI-powered solution for interview preparation that combines cutting-edge technology with user-centric design. The platform leverages Google's Gemini AI to provide personalized, realistic interview experiences that help candidates improve their skills and confidence.

### Key Strengths

1. **Intelligent AI Integration**: Advanced use of Google's Generative AI for CV parsing, question generation, and answer evaluation
2. **Modern Architecture**: Clean separation of concerns with microservices architecture
3. **Dual Interview Modes**: Flexibility with both text and voice-based interviews
4. **Comprehensive Feedback**: Detailed, actionable reports to drive improvement
5. **User-Friendly Interface**: Intuitive React-based frontend with modern design
6. **Scalable Infrastructure**: Docker-based deployment ready for growth
7. **Developer-Friendly**: Well-structured codebase with clear documentation

### Use Cases

- **Job Seekers**: Practice interviews for target positions
- **Career Changers**: Prepare for new industry interviews
- **Students**: Prepare for internship and entry-level interviews
- **Professionals**: Sharpen interview skills for promotions
- **Recruiters**: Understand candidate preparation tools
- **Educational Institutions**: Provide career services to students

### Project Maturity

EnterVU is a production-ready application with:
- Stable core functionality
- Comprehensive feature set
- Active development
- Clear roadmap for enhancements
- Strong foundation for future growth

---

## Contact & Support

For questions, issues, or contributions:
- **Repository**: https://github.com/bilel-amri0/EnterVU-main
- **Issues**: GitHub Issues for bug reports and feature requests
- **License**: Apache License 2.0

---

**Last Updated**: November 2024  
**Version**: 1.0.0  
**Status**: Active Development
