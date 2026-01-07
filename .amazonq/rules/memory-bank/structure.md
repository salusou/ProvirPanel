# Provir Cloud Panel - Project Structure

## Directory Organization

### Root Level Structure
```
ProvirPanel/
├── backend/                 # Node.js Express API server
├── frontend/               # React + Vite client application
├── nginx/                  # Nginx reverse proxy configuration
├── .amazonq/              # Amazon Q IDE integration rules
├── install-*.sh           # Platform-specific installation scripts
├── docker-compose.yml     # Container orchestration setup
└── package.json          # Root project configuration
```

### Backend Architecture (`/backend/`)
```
backend/
├── src/
│   ├── server.js          # Main Express application entry point
│   ├── config/
│   │   ├── database.js    # PostgreSQL connection configuration
│   │   └── schema.sql     # Database schema definitions
│   ├── routes/
│   │   ├── auth.js        # Authentication endpoints
│   │   ├── metrics.js     # System metrics API
│   │   ├── terminal.js    # Terminal session management
│   │   ├── docker.js      # Container management API
│   │   ├── storage.js     # File system operations
│   │   └── ci-cd.js       # Deployment pipeline API
│   ├── services/
│   │   ├── CommandExecutor.js    # Terminal command execution
│   │   ├── MetricsCollector.js   # System monitoring service
│   │   ├── DockerManager.js      # Docker API wrapper
│   │   ├── StorageManager.js     # File operations service
│   │   └── CICDManager.js        # Deployment automation
│   └── middleware/
│       ├── auth.js        # JWT authentication middleware
│       └── errorHandler.js # Global error handling
├── data/                  # Runtime data storage
│   ├── projects/          # User project files
│   ├── docker-services.json
│   ├── domains.json
│   └── proxy-routes.json
├── logs/                  # Application logs
└── .env                   # Environment configuration
```

### Frontend Architecture (`/frontend/`)
```
frontend/
├── src/
│   ├── main.jsx           # React application entry point
│   ├── App.jsx            # Root component with routing
│   ├── components/
│   │   ├── Dashboard.jsx  # Main dashboard with metrics
│   │   ├── Terminal.jsx   # Web terminal interface
│   │   ├── DockerPanel.jsx # Container management UI
│   │   ├── FileManager.jsx # File explorer and editor
│   │   ├── Navbar.jsx     # Top navigation bar
│   │   └── Sidebar.jsx    # Side navigation menu
│   ├── pages/
│   │   ├── LoginPage.jsx  # Authentication interface
│   │   └── MainLayout.jsx # Main application layout
│   ├── services/
│   │   ├── api.js         # HTTP API client
│   │   └── socket.js      # WebSocket client
│   └── assets/            # Static assets and styles
├── public/                # Public static files
├── package.json          # Frontend dependencies
├── vite.config.js        # Vite build configuration
├── tailwind.config.js    # Tailwind CSS configuration
└── eslint.config.js      # ESLint code quality rules
```

## Core Components & Relationships

### Backend Service Layer
- **Express Server**: RESTful API with middleware pipeline
- **Socket.io Integration**: Real-time bidirectional communication
- **PostgreSQL Database**: User management and application state
- **Service Classes**: Modular business logic implementation

### Frontend Component Hierarchy
- **App.jsx**: Root router and authentication context
- **MainLayout.jsx**: Authenticated user interface shell
- **Feature Components**: Dashboard, Terminal, Docker, FileManager
- **Shared Services**: API client and WebSocket management

### Data Flow Architecture
1. **Authentication Flow**: JWT tokens for stateless authentication
2. **API Communication**: RESTful endpoints for CRUD operations
3. **Real-time Updates**: WebSocket events for live data streaming
4. **File Operations**: Multer middleware for file upload handling
5. **Container Management**: Dockerode library for Docker API integration

## Architectural Patterns

### Backend Patterns
- **MVC Architecture**: Routes → Services → Database
- **Middleware Pipeline**: Authentication, CORS, error handling
- **Service Layer Pattern**: Business logic separation
- **Repository Pattern**: Database access abstraction

### Frontend Patterns
- **Component-Based Architecture**: Reusable React components
- **Service Layer**: API and WebSocket abstraction
- **State Management**: React hooks and context
- **Responsive Design**: Tailwind CSS utility classes

### Communication Patterns
- **RESTful API**: Standard HTTP methods for resource operations
- **WebSocket Events**: Real-time data streaming and terminal I/O
- **File Streaming**: Multipart uploads and binary downloads
- **Error Handling**: Centralized error responses and logging

## Integration Points

### External Dependencies
- **Docker Engine**: Container lifecycle management
- **PostgreSQL**: Persistent data storage
- **Git Repositories**: Source code management for CI/CD
- **System Commands**: OS-level operations via child processes

### Internal Integrations
- **Authentication Middleware**: JWT validation across all protected routes
- **WebSocket Namespaces**: Organized real-time communication channels
- **File System Access**: Secure project directory management
- **Process Management**: PM2 for production deployment

### Configuration Management
- **Environment Variables**: Runtime configuration via .env files
- **Database Schema**: SQL migrations and table definitions
- **Nginx Configuration**: Reverse proxy and static file serving
- **Docker Compose**: Multi-container application orchestration