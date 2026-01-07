# Provir Cloud Panel - Development Guidelines

## Code Quality Standards

### JavaScript/Node.js Backend Standards
- **Strict Mode**: Always use `'use strict';` at the top of Node.js modules
- **CommonJS Modules**: Use `require()` and `module.exports` for backend modules
- **Async/Await**: Prefer async/await over Promise chains for better readability
- **Error Handling**: Use try-catch blocks and proper error propagation
- **Environment Variables**: Load configuration via `dotenv` with explicit path resolution
- **Database Connections**: Use connection pooling with `pg.Pool` for PostgreSQL

### React/Frontend Standards
- **ES Modules**: Use `import/export` syntax for frontend modules
- **JSX Extensions**: Use `.jsx` extension for React components
- **Functional Components**: Prefer function components over class components
- **Hooks Pattern**: Use React hooks (useState, useEffect, useCallback) for state management
- **Component Naming**: Use PascalCase for component names and files

### Code Formatting Patterns
- **Indentation**: 2-space indentation consistently across all files
- **Semicolons**: Use semicolons in backend code, optional in frontend with ESLint rules
- **Quotes**: Single quotes for strings in backend, flexible in frontend
- **Line Length**: Keep lines reasonable length, break long parameter lists
- **Trailing Commas**: Use trailing commas in multi-line objects and arrays

## Structural Conventions

### File Organization Patterns
- **Route Handlers**: Separate route definitions from business logic
- **Service Layer**: Extract business logic into dedicated service classes
- **Middleware**: Create reusable middleware for cross-cutting concerns
- **Configuration**: Centralize configuration in dedicated config files
- **Component Structure**: Group related components in feature-based directories

### Naming Conventions
- **Files**: kebab-case for route files, PascalCase for React components
- **Variables**: camelCase for variables and functions
- **Constants**: UPPER_SNAKE_CASE for environment variables and constants
- **Database**: snake_case for table and column names
- **API Endpoints**: RESTful naming with plural nouns

### Import/Export Patterns
```javascript
// Backend - CommonJS
const express = require('express');
const { Pool } = require('pg');
module.exports = router;

// Frontend - ES Modules
import { useState, useEffect } from 'react'
import api from './services/api.js'
export default Component
```

## Practices Followed Throughout Codebase

### Authentication & Security
- **JWT Tokens**: Stateless authentication with configurable expiration
- **Password Hashing**: bcrypt with salt rounds of 12 for security
- **Middleware Protection**: Apply auth middleware to protected routes
- **CORS Configuration**: Configurable CORS origins via environment variables
- **Security Headers**: Use helmet middleware for security headers

### Database Interaction Patterns
```javascript
// Connection pooling
const pool = new Pool({
  connectionString: process.env.DATABASE_URL,
  ssl: process.env.DATABASE_SSL === 'true' ? { rejectUnauthorized: false } : false
});

// Parameterized queries
await pool.query('SELECT * FROM users WHERE username = $1', [username]);
```

### Error Handling Strategies
- **Centralized Error Handler**: Global error middleware for consistent responses
- **Graceful Degradation**: Continue operation when non-critical services fail
- **Logging**: Use console methods with appropriate log levels
- **Client Error Handling**: Catch API errors and provide user feedback

### Socket.io Integration
- **Namespace Organization**: Separate namespaces for different features
- **Event Naming**: Descriptive event names (metrics, terminal-output, docker-logs)
- **Connection Management**: Proper cleanup on disconnect events
- **Real-time Updates**: 5-second intervals for metrics broadcasting

## Semantic Patterns Overview

### API Design Patterns
- **RESTful Endpoints**: Standard HTTP methods (GET, POST, PUT, DELETE)
- **Route Grouping**: Organize routes by feature (/auth, /api/metrics, /docker)
- **Middleware Chain**: Authentication → Feature Logic → Error Handling
- **Response Format**: Consistent JSON responses with status and data

### React Component Patterns
```javascript
// Functional component with hooks
const Component = () => {
  const [state, setState] = useState(initialValue)
  
  useEffect(() => {
    // Side effects
    return () => {
      // Cleanup
    }
  }, [dependencies])
  
  return <JSX />
}
```

### State Management Patterns
- **Local State**: useState for component-specific state
- **Effect Hooks**: useEffect for side effects and cleanup
- **Callback Optimization**: useCallback for stable function references
- **Authentication Context**: Global auth state via React context

### Async Operation Patterns
```javascript
// Backend async/await
const handleRequest = async (req, res) => {
  try {
    const result = await service.operation()
    res.json({ success: true, data: result })
  } catch (error) {
    res.status(500).json({ error: error.message })
  }
}

// Frontend API calls
const fetchData = async () => {
  try {
    const response = await api.get('/endpoint')
    setData(response.data)
  } catch (error) {
    setError(error.message)
  }
}
```

## Internal API Usage Patterns

### Express Application Setup
```javascript
const app = express()
app.use(helmet())
app.use(cors())
app.use(express.json())
app.use('/api/endpoint', authMiddleware, routes)
app.use(errorHandler)
```

### Socket.io Server Integration
```javascript
const io = new Server(server, {
  cors: { origin: process.env.CORS_ORIGIN || '*' }
})

io.on('connection', (socket) => {
  socket.emit('connected', { message: 'Socket connected' })
  socket.on('event', handleEvent)
})
```

### Database Query Patterns
```javascript
// Simple query
const result = await pool.query('SELECT * FROM table WHERE id = $1', [id])

// Transaction handling
const client = await pool.connect()
try {
  await client.query('BEGIN')
  await client.query('INSERT INTO...', values)
  await client.query('COMMIT')
} catch (error) {
  await client.query('ROLLBACK')
  throw error
} finally {
  client.release()
}
```

### React Router Integration
```javascript
// Protected route wrapper
const ProtectedRoute = ({ children }) => {
  if (!authenticated) return <Navigate to="/login" replace />
  return children
}

// Route configuration
<Routes>
  <Route path="/login" element={<PublicRoute><LoginPage /></PublicRoute>} />
  <Route path="/" element={<ProtectedRoute><MainLayout /></ProtectedRoute>}>
    <Route index element={<Dashboard />} />
    <Route path="feature" element={<FeatureComponent />} />
  </Route>
</Routes>
```

## Frequently Used Code Idioms

### Environment Configuration
```javascript
// Backend configuration loading
require('dotenv').config({ path: path.join(__dirname, '../.env') })
const port = process.env.PORT || 3000

// Frontend API base URL
const API_BASE = process.env.VITE_API_URL || 'http://localhost:3000'
```

### Conditional Rendering Patterns
```javascript
// Loading states
if (loading) return <LoadingSpinner />
if (error) return <ErrorMessage error={error} />

// Conditional classes
className={`base-class ${condition ? 'active' : 'inactive'}`}
```

### Service Class Patterns
```javascript
class ServiceClass {
  constructor() {
    this.client = new ExternalClient()
  }
  
  async operation() {
    try {
      return await this.client.method()
    } catch (error) {
      throw new Error(`Operation failed: ${error.message}`)
    }
  }
}
```

## Popular Annotations & Comments

### ESLint Directives
```javascript
// Disable specific rules when necessary
// eslint-disable-next-line no-console
console.log('Development logging')

// Global ignores in config
globalIgnores: ['dist']
```

### Documentation Comments
```javascript
// Configuration comments
// https://vite.dev/config/
export default defineConfig({...})

// Intentional behavior comments
// Intentionally left blank for now.
// Intentionally ignore metrics errors for now.
```

### TODO and Implementation Notes
- Use descriptive comments for complex business logic
- Document API endpoint purposes and expected parameters
- Explain non-obvious configuration choices
- Mark intentional empty blocks to avoid confusion