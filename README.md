# AMC-Dashboard

A comprehensive dashboard application for managing Annual Maintenance Contracts (AMC), purchase orders, and user management. This full-stack application provides a robust platform for businesses to streamline their maintenance contract operations, manage purchase orders, and handle user administration efficiently.

## 📖 Table of Contents
- [Features](#-features)
- [Technical Architecture](#-technical-architecture)
- [Component Documentation](#-component-documentation)
- [State Management](#-state-management)
- [Database Schema](#-database-schema)
- [API Documentation](#-api-documentation)
- [Security Implementation](#-security-implementation)
- [Installation](#-installation)
- [Development](#-development)
- [Deployment](#-deployment)
- [Contributing](#-contributing)

## 🏛️ Technical Architecture

### Frontend Architecture
The frontend follows a component-based architecture using React and TypeScript, ensuring type safety and better development experience.

#### Key Technical Decisions:
- **Vite**: Chosen for its fast build times and efficient development server
- **TypeScript**: Ensures type safety and better code maintainability
- **Tailwind CSS**: Provides utility-first CSS framework for responsive design
- **Context API**: Manages global state without additional dependencies

### Directory Structure Explained
```
src/
├── components/           # Reusable UI components
│   ├── Auth/            # Authentication related components
│   ├── Contracts/       # Contract management components
│   ├── Dashboard/       # Dashboard views
│   ├── Layout/          # Layout components
│   ├── Profile/         # User profile components
│   ├── PurchaseOrders/  # Purchase order related components
│   ├── UI/              # Shared UI components
│   └── Users/           # User management components
├── contexts/            # Global state management
└── assets/             # Static files
```

### Backend Architecture
The backend implements a layered architecture pattern:

```
server/
├── routes/             # Route definitions and request handling
├── middleware/         # Custom middleware (auth, validation)
├── services/          # Business logic layer
└── index.js           # Application entry point
```

## 🧩 Component Documentation

### Authentication Components
1. **Login (`Login.tsx`)**
   - Handles user authentication
   - Implements JWT token management
   - Features remember me functionality
   - Provides form validation

2. **Register (`Register.tsx`)**
   - New user registration
   - Email verification
   - Password strength validation
   - Form validation using TypeScript

3. **ForgotPassword (`ForgotPassword.tsx`)**
   - Password recovery workflow
   - Email notification system
   - Security questions handling

### Dashboard Components
1. **Dashboard (`Dashboard.tsx`)**
   - Main application interface
   - Data visualization components
   - Quick action buttons
   - Status overview panels

### Contract Management
1. **ContractForm (`ContractForm.tsx`)**
   - Contract creation/editing interface
   - Dynamic form validation
   - File attachment handling
   - Contract template selection

2. **ContractList (`ContractList.tsx`)**
   - Paginated contract display
   - Sorting and filtering
   - Bulk actions
   - Export functionality

### Purchase Order Components
1. **PurchaseOrderForm (`PurchaseOrderForm.tsx`)**
   - Purchase order creation
   - Dynamic line items
   - Total calculation
   - Vendor selection

2. **PurchaseOrderList (`PurchaseOrderList.tsx`)**
   - Order status tracking
   - Filter and search
   - Export to PDF/Excel
   - Bulk operations

## 🔄 State Management

### Authentication Context
```typescript
interface AuthState {
  user: User | null;
  isAuthenticated: boolean;
  loading: boolean;
  error: string | null;
}

interface AuthContext {
  login: (credentials: LoginCredentials) => Promise<void>;
  logout: () => void;
  updateUser: (userData: Partial<User>) => Promise<void>;
}
```

### Key State Management Features:
- Centralized authentication state
- User session management
- Token refresh mechanism
- Error handling

## 🗃️ Database Schema

### Core Tables
1. **Users**
   ```prisma
   model User {
     id        Int      @id @default(autoincrement())
     email     String   @unique
     name      String
     role      Role     @default(USER)
     contracts Contract[]
     createdAt DateTime @default(now())
     updatedAt DateTime @updatedAt
   }
   ```

2. **Contracts**
   ```prisma
   model Contract {
     id          Int      @id @default(autoincrement())
     title       String
     startDate   DateTime
     endDate     DateTime
     value       Decimal
     clientId    Int
     status      Status
     createdById Int
     createdAt   DateTime @default(now())
     updatedAt   DateTime @updatedAt
   }
   ```

3. **Purchase Orders**
   ```prisma
   model PurchaseOrder {
     id          Int      @id @default(autoincrement())
     poNumber    String   @unique
     vendorId    Int
     totalAmount Decimal
     status      POStatus
     items       POItem[]
     createdAt   DateTime @default(now())
     updatedAt   DateTime @updatedAt
   }
   ```

## 🔒 Security Implementation

### Authentication Flow
1. JWT-based authentication
2. Token refresh mechanism
3. Password hashing using bcrypt
4. Rate limiting on auth endpoints

### Security Measures
- CORS configuration
- XSS protection
- CSRF tokens
- Input validation
- SQL injection prevention
- File upload validation

## 🚀 Features

- **Authentication System**
  - User registration and login
  - Password reset functionality
  - Secure authentication middleware
  - Protected routes

- **Contract Management**
  - Create and manage AMC contracts
  - View contract listings
  - Track contract status

- **Purchase Order System**
  - Create purchase orders
  - Track purchase order status
  - View purchase order history

- **User Management**
  - User roles and permissions
  - User profile management
  - User listing and administration

## 🛠️ Tech Stack

- **Frontend**
  - React with TypeScript
  - Vite (Build tool)
  - Tailwind CSS (Styling)
  - Context API for state management

- **Backend**
  - Node.js
  - Express.js
  - Prisma (ORM)
  - PostgreSQL (Database)

## 📦 Prerequisites

- Node.js (v16 or higher)
- PostgreSQL
- npm or yarn

## 🔧 Installation

### Prerequisites
1. **Node.js and npm**
   - Node.js version 16.x or higher
   - npm version 7.x or higher

2. **Database**
   - PostgreSQL 13.x or higher
   - Create a new database named `amc_dashboard`

3. **Development Tools**
   - Git
   - VS Code (recommended)
   - Postman (for API testing)

### Installation Steps

1. **Clone the repository:**
```bash
git clone https://github.com/Parikshit2304/AMC-Dashboard.git
cd AMC-Dashboard
```

2. **Install dependencies:**
```bash
# Install frontend dependencies
npm install

# Install backend dependencies
cd server
npm install
```

3. **VS Code Extensions (Recommended)**
   - ESLint
   - Prettier
   - Tailwind CSS IntelliSense
   - Prisma
   - GitLens

4. **Environment Setup**
   Create the following `.env` files:

   Root directory `.env`:
   ```env
   VITE_API_URL=http://localhost:3000
   VITE_ENV=development
   ```

   Server directory `.env`:
   ```env
   PORT=3000
   NODE_ENV=development
   DATABASE_URL="postgresql://username:password@localhost:5432/amc_dashboard"
   JWT_SECRET="your-secure-jwt-secret"
   JWT_EXPIRE="24h"
   SMTP_HOST="your-smtp-host"
   SMTP_PORT=587
   SMTP_USER="your-smtp-user"
   SMTP_PASS="your-smtp-password"
   ```

3. Set up environment variables:
Create a `.env` file in the root directory and add:
```env
DATABASE_URL="postgresql://username:password@localhost:5432/amc_dashboard"
JWT_SECRET="your-secret-key"
```

4. Set up the database:
```bash
npx prisma migrate dev
npm run seed
```

## 🚀 Development

### Setting Up Development Environment

1. **Database Setup**
```bash
# Navigate to project root
cd AMC-Dashboard

# Generate Prisma client
npx prisma generate

# Run migrations
npx prisma migrate dev

# Seed the database
npm run seed
```

2. **Starting Development Servers**

Start the backend server:
```bash
cd server
npm run dev
```

In a new terminal, start the frontend:
```bash
# From project root
npm run dev
```

The application will be available at:
- Frontend: `http://localhost:5173`
- Backend API: `http://localhost:3000`

### Development Commands

```bash
# Run tests
npm run test

# Run tests with coverage
npm run test:coverage

# Lint code
npm run lint

# Format code
npm run format

# Type check
npm run type-check

# Build for production
npm run build
```

### Development Guidelines

1. **Code Style**
   - Follow ESLint configuration
   - Use Prettier for formatting
   - Follow TypeScript strict mode guidelines

2. **Git Workflow**
   - Create feature branches from `develop`
   - Use conventional commits
   - Submit PRs for review

3. **Testing Requirements**
   - Unit tests for utilities and hooks
   - Integration tests for API endpoints
   - E2E tests for critical flows

## 📦 Deployment

### Production Build

1. **Frontend Build**
```bash
npm run build
```

2. **Backend Build**
```bash
cd server
npm run build
```

### Deployment Options

1. **Docker Deployment**
```bash
# Build Docker images
docker-compose build

# Run containers
docker-compose up -d
```

2. **Manual Deployment**
   - Set up Node.js environment
   - Configure nginx/Apache
   - Set up SSL certificates
   - Configure environment variables

### Production Considerations
- Enable rate limiting
- Set up monitoring (e.g., Sentry)
- Configure backup strategy
- Set up CI/CD pipeline

## 🏗️ Project Structure

```
AMC-Dashboard/
├── src/                    # Frontend source code
│   ├── components/         # React components
│   ├── contexts/          # React contexts
│   └── assets/           # Static assets
├── server/                # Backend source code
│   ├── routes/           # API routes
│   ├── middleware/       # Express middleware
│   └── services/         # Business logic
└── prisma/               # Database schema and migrations
```

## � API Documentation

### Authentication Endpoints

#### Register User
```http
POST /api/auth/register
Content-Type: application/json

{
  "name": "string",
  "email": "string",
  "password": "string",
  "role": "USER | ADMIN"
}

Response: 201 Created
{
  "user": {
    "id": "number",
    "name": "string",
    "email": "string",
    "role": "string"
  },
  "token": "string"
}
```

#### Login
```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "string",
  "password": "string",
  "rememberMe": "boolean"
}

Response: 200 OK
{
  "token": "string",
  "user": {
    "id": "number",
    "name": "string",
    "email": "string",
    "role": "string"
  }
}
```

#### Password Reset
```http
POST /api/auth/forgot-password
Content-Type: application/json

{
  "email": "string"
}

Response: 200 OK
{
  "message": "Password reset email sent"
}
```

### Contract Management Endpoints

#### List Contracts
```http
GET /api/contracts
Authorization: Bearer {token}
Query Parameters:
  - page: number
  - limit: number
  - status: "ACTIVE | EXPIRED | PENDING"
  - sortBy: "createdAt | value | startDate"
  - order: "ASC | DESC"

Response: 200 OK
{
  "contracts": [
    {
      "id": "number",
      "title": "string",
      "startDate": "date",
      "endDate": "date",
      "value": "number",
      "status": "string"
    }
  ],
  "total": "number",
  "page": "number",
  "totalPages": "number"
}
```

#### Create Contract
```http
POST /api/contracts
Authorization: Bearer {token}
Content-Type: application/json

{
  "title": "string",
  "startDate": "date",
  "endDate": "date",
  "value": "number",
  "clientId": "number",
  "terms": "string"
}

Response: 201 Created
{
  "id": "number",
  "title": "string",
  "startDate": "date",
  "endDate": "date",
  "value": "number",
  "status": "string"
}
```

### Purchase Order Endpoints

#### List Purchase Orders
```http
GET /api/purchase-orders
Authorization: Bearer {token}
Query Parameters:
  - page: number
  - limit: number
  - status: "DRAFT | PENDING | APPROVED | COMPLETED"
  - vendor: "number"
  - dateFrom: "date"
  - dateTo: "date"

Response: 200 OK
{
  "purchaseOrders": [
    {
      "id": "number",
      "poNumber": "string",
      "vendorId": "number",
      "totalAmount": "number",
      "status": "string",
      "createdAt": "date"
    }
  ],
  "total": "number",
  "page": "number",
  "totalPages": "number"
}
```

#### Create Purchase Order
```http
POST /api/purchase-orders
Authorization: Bearer {token}
Content-Type: application/json

{
  "vendorId": "number",
  "items": [
    {
      "description": "string",
      "quantity": "number",
      "unitPrice": "number"
    }
  ],
  "notes": "string"
}

Response: 201 Created
{
  "id": "number",
  "poNumber": "string",
  "totalAmount": "number",
  "status": "string",
  "items": [
    {
      "id": "number",
      "description": "string",
      "quantity": "number",
      "unitPrice": "number",
      "total": "number"
    }
  ]
}
```

### Error Responses

```http
400 Bad Request
{
  "error": "string",
  "details": object | array
}

401 Unauthorized
{
  "error": "Authentication required"
}

403 Forbidden
{
  "error": "Insufficient permissions"
}

404 Not Found
{
  "error": "Resource not found"
}

500 Internal Server Error
{
  "error": "Internal server error"
}
```

## 👥 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👤 Author

Parikshit2304

## 🙏 Acknowledgments

- React Team
- Vite Team
- Tailwind CSS Team
- Prisma Team