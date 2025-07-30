# CollabTask
CollabTask - Real-Time Collaborative Task Management App
CollabTask is a high-end, full-stack web application for team task management with real-time collaboration, inspired by tools like Trello. It features drag-and-drop task boards, AI-powered task suggestions, secure authentication, and a scalable microservices-inspired architecture.
Features

User Authentication: Register/login with email/password or OAuth (Google/GitHub).
Boards & Tasks: Create/edit/delete boards and tasks with titles, descriptions, due dates, assignees, and statuses (To Do, In Progress, Done).
Real-Time Collaboration: Multi-user editing with live updates via WebSockets.
AI Suggestions: Generate task breakdowns using OpenAI's API through a FastAPI microservice.
Search & Filtering: Full-text search and filters by assignee, status, etc.
Export & Notifications: Export boards to PDF/CSV; email notifications.
Responsive UI: Mobile-first design with Tailwind CSS and Shadcn/UI.
Scalable & Secure: Microservices-inspired monolith, JWT auth, Redis caching, rate limiting.

Tech Stack

Frontend: Next.js 14 (React + TypeScript), Tailwind CSS, Shadcn/UI, React DnD, Socket.io Client
Backend: Node.js + Express.js, Sequelize (PostgreSQL), Redis, Socket.io Server, JWT, Passport.js
AI Microservice: FastAPI (Python), OpenAI API
Databases: PostgreSQL 16, Redis 7
DevOps: Docker, Docker Compose, GitHub Actions (CI/CD), Vercel/AWS
Testing: Jest, React Testing Library, Mocha, Supertest, Cypress

Prerequisites

Node.js 18+
Python 3.10+
Docker & Docker Compose
PostgreSQL 16
Redis 7
OpenAI API key (for AI features)
Git

Setup Instructions

Clone the Repository:
git clone https://github.com/your-username/collabtask.git
cd collabtask


Environment Variables:

Copy .env.example to .env in backend/, frontend/, and ai-service/.
Fill in required variables:
backend/.env: DATABASE_URL=postgres://user:pass@localhost:5432/collabtask, JWT_SECRET, REDIS_URL
frontend/.env.local: NEXT_PUBLIC_API_URL=http://localhost:5000, NEXT_PUBLIC_SOCKET_URL=http://localhost:5000
ai-service/.env: OPENAI_API_KEY=your_openai_key




Install Dependencies:
# Backend
cd backend
npm install
# Frontend
cd ../frontend
npm install
# AI Service
cd ../ai-service
pip install -r requirements.txt


Database Setup:

Start PostgreSQL and Redis via Docker:docker-compose up -d postgres redis


Run migrations in backend/:npx sequelize-cli db:migrate




Run Locally:

Start all services with Docker Compose:docker-compose up --build


Or run individually:
Backend: cd backend && npm run dev (runs on http://localhost:5000)
Frontend: cd frontend && npm run dev (runs on http://localhost:3000)
AI Service: cd ai-service && uvicorn main:app --reload (runs on http://localhost:8000)




Access the App:

Frontend: http://localhost:3000
API: http://localhost:5000/api
API Docs: http://localhost:5000/api-docs (Swagger, if enabled)
AI Service: http://localhost:8000/docs (FastAPI Swagger UI)



Development

Code Style: ESLint + Prettier; enforced via Husky pre-commit hooks.
Testing:
Backend: cd backend && npm test (Mocha/Supertest)
Frontend: cd frontend && npm test (Jest/RTL)
E2E: cd frontend && npx cypress open (Cypress)


Real-Time Features: Uses Socket.io for live task updates. Join boards via /board/:id.
AI Integration: POST to http://localhost:8000/suggest-tasks with a prompt to get task suggestions.

Deployment

Docker:
Build and push images: docker-compose build && docker-compose push
Deploy to AWS ECS or similar for backend/ai-service; Vercel for frontend.


CI/CD:
GitHub Actions workflows in .github/workflows/ci.yml handle linting, testing, and deployment.


Cloud Setup:
Frontend: Vercel (set NEXT_PUBLIC_* env vars).
Backend: AWS EC2/ECS with RDS (PostgreSQL) and ElastiCache (Redis).
AI Service: AWS Lambda or ECS for FastAPI.



Project Structure
collabtask/
├── backend/                # Express.js API + Socket.io
├── frontend/               # Next.js app
├── ai-service/             # FastAPI for AI task suggestions
├── docker-compose.yml      # Orchestrates services
├── .github/workflows/      # CI/CD pipelines
└── README.md

Contributing

Fork the repo.
Create a feature branch: git checkout -b feature/your-feature.
Commit changes: git commit -m "Add your feature".
Push and open a PR: git push origin feature/your-feature.

License
MIT License. See LICENSE for details.
Acknowledgments
Inspired by open-source projects like Worklenz, Plane, and collaborative-task-manager.
