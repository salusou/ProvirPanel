# Provir Cloud Panel - Technology Stack

## Programming Languages & Versions

### Backend Technologies
- **Node.js**: 18+ (JavaScript runtime)
- **JavaScript**: ES2020+ with modern async/await patterns
- **SQL**: PostgreSQL-compatible schema and queries
- **Shell Script**: Bash for installation and deployment automation

### Frontend Technologies
- **JavaScript**: ES2020+ with JSX syntax
- **CSS**: Tailwind CSS utility classes
- **HTML**: React JSX templates
- **TypeScript**: Type definitions for development tooling

## Core Dependencies

### Backend Stack
```json
{
  "express": "^4.19.2",           // Web application framework
  "socket.io": "^4.7.5",         // Real-time bidirectional communication
  "pg": "^8.11.5",               // PostgreSQL client
  "dockerode": "^4.0.0",         // Docker Engine API client
  "jsonwebtoken": "^9.0.2",      // JWT authentication
  "bcrypt": "^5.1.1",            // Password hashing
  "multer": "^1.4.5-lts.1",      // File upload middleware
  "cors": "^2.8.5",              // Cross-origin resource sharing
  "helmet": "^7.1.0",            // Security headers middleware
  "dotenv": "^16.4.5",           // Environment variable loading
  "axios": "^1.6.0",             // HTTP client for external APIs
  "tar-fs": "^3.0.4"             // File system archive operations
}
```

### Frontend Stack
```json
{
  "react": "^19.2.0",                    // UI component library
  "react-dom": "^19.2.0",               // React DOM rendering
  "react-router-dom": "^7.11.0",        // Client-side routing
  "vite": "^7.2.4",                     // Build tool and dev server
  "tailwindcss": "^3.4.13",             // Utility-first CSS framework
  "@monaco-editor/react": "^4.6.0",     // Code editor component
  "xterm": "^5.3.0",                    // Terminal emulator
  "socket.io-client": "^4.8.3",         // WebSocket client
  "axios": "^1.13.2",                   // HTTP client
  "recharts": "^3.6.0",                 // Chart and visualization library
  "lucide-react": "^0.562.0"            // Icon component library
}
```

## Build Systems & Tools

### Development Tools
- **Vite**: Frontend build tool with hot module replacement
- **ESLint**: Code quality and style enforcement
- **PostCSS**: CSS processing with Autoprefixer
- **Tailwind CSS**: Utility-first styling framework
- **PM2**: Production process manager for Node.js

### Database & Infrastructure
- **PostgreSQL**: 12+ relational database
- **Docker**: Container platform for service isolation
- **Nginx**: Reverse proxy and static file server
- **Git**: Version control for CI/CD integration

## Development Commands

### Backend Development
```bash
# Install dependencies
npm install

# Start development server with auto-reload
npm run dev

# Start production server
npm run start

# Start with PM2 process manager
npm run pm2:start
```

### Frontend Development
```bash
# Navigate to frontend directory
cd frontend

# Install dependencies
npm install

# Start development server (http://localhost:5173)
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Run code linting
npm run lint
```

### Database Operations
```bash
# Connect to PostgreSQL
psql "$DATABASE_URL"

# Initialize database schema
psql "$DATABASE_URL" -f backend/src/config/schema.sql

# Create database user and permissions
sudo -u postgres psql -c "CREATE ROLE provirpanel LOGIN PASSWORD 'password';"
sudo -u postgres createdb -O provirpanel provirpanel
```

### Docker Operations
```bash
# Start all services with Docker Compose
docker-compose up -d

# View service logs
docker-compose logs -f

# Stop all services
docker-compose down

# Rebuild and restart services
docker-compose up -d --build
```

## Environment Configuration

### Backend Environment Variables (.env)
```bash
PORT=3000                                    # Server port
DATABASE_URL=postgres://user:pass@host/db   # PostgreSQL connection
DATABASE_SSL=false                          # SSL mode for database
CORS_ORIGIN=*                              # CORS allowed origins
JWT_SECRET=your-secret-key                  # JWT signing secret
JWT_EXPIRES_IN=1d                          # Token expiration time
CLOUDPAINEL_PROJECTS_DIR=/path/to/projects  # File storage directory
DEFAULT_ADMIN_USER=admin                    # Initial admin username
DEFAULT_ADMIN_PASS=admin123                # Initial admin password
TERMINAL_OS_USER=provirpanel               # OS user for terminal commands
```

### Frontend Build Configuration
- **Vite Config**: Development server and build optimization
- **Tailwind Config**: CSS utility configuration and theming
- **ESLint Config**: Code quality rules and React-specific linting
- **PostCSS Config**: CSS processing pipeline

## Platform Support

### Supported Operating Systems
- **Linux**: Debian/Ubuntu, RHEL/CentOS/Rocky/AlmaLinux, SUSE/openSUSE
- **macOS**: Intel and Apple Silicon architectures
- **FreeBSD**: Unix-like system support
- **Windows Server**: PowerShell-based installation

### Installation Methods
- **Automated Scripts**: Platform-specific shell/PowerShell installers
- **Docker Compose**: Containerized deployment
- **Manual Setup**: Step-by-step development environment
- **Package Managers**: npm, apt, yum, dnf, zypper support

## Development Workflow

### Local Development Setup
1. Install Node.js 18+ and PostgreSQL 12+
2. Clone repository and install dependencies
3. Configure environment variables
4. Initialize database schema
5. Start backend and frontend development servers

### Production Deployment
1. Run platform-specific installation script
2. Automated dependency installation and configuration
3. Database setup and user creation
4. Nginx reverse proxy configuration
5. PM2 process management setup
6. SSL certificate configuration (optional)

### CI/CD Integration
- Git webhook support for automated deployments
- Build script execution and dependency management
- Process restart and health checking
- Rollback capabilities for failed deployments
- Deploy history and logging