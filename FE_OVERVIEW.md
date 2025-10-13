# Jobs Admin Console - Applicant Tracking System

A modern React-based admin console for managing job postings, applications, candidates, and company profiles. This application provides a comprehensive interface for HR teams and recruiters to streamline their hiring processes.

## 🚀 Tech Stack

### Frontend Framework
- **React 18.2.0** - Modern React with hooks and functional components
- **TypeScript 4.9.5** - Type-safe JavaScript development
- **React Router DOM 6.30.1** - Client-side routing and navigation

### UI & Styling
- **Ant Design 5.20.3** - Enterprise-class UI design language and components
- **Tailwind CSS 3.4.12** - Utility-first CSS framework
- **Ant Design Icons 5.4.0** - Comprehensive icon library
- **FontAwesome** - Additional icon sets for enhanced UI

### State Management & Data Flow
- **Zustand 4.5.5** - Lightweight state management with persistence
- **RxJS 7.8.1** - Reactive programming for complex async operations
- **CryptoJS 4.2.0** - Encrypted local storage for sensitive data

### Development Tools
- **Create React App 5.0.1** - Zero-configuration React development environment
- **Husky 9.1.7** - Git hooks for code quality enforcement
- **Prettier 3.5.3** - Code formatting with Tailwind plugin
- **ESLint** - Code linting and quality assurance

### Additional Libraries
- **React Quill 2.0.0** - Rich text editor for job descriptions
- **React Select 5.9.0** - Enhanced select components
- **SweetAlert2** - Beautiful, responsive alert dialogs
- **React Input Mask** - Input formatting and validation
- **DND Kit** - Drag and drop functionality

## 🏗️ Project Structure

```
src/
├── assets/                     # Static assets (images, icons, data)
│   ├── logo.png
│   ├── logo.svg
│   └── countries.json
├── constants/                  # Application constants
│   └── routes.ts              # Route definitions and prefixes
├── core/                      # Core application infrastructure
│   ├── components/            # Reusable UI components
│   │   ├── Button.tsx
│   │   ├── Input.tsx
│   │   ├── Table/
│   │   ├── Dropdown.tsx
│   │   └── ...
│   ├── constants/             # Design system constants
│   │   ├── colors.ts
│   │   ├── sizes.ts
│   │   └── weights.ts
│   ├── guards/                # Route protection
│   │   └── private.guard.tsx
│   ├── interfaces/            # TypeScript interfaces
│   ├── models/                # Data models and types
│   │   ├── auth/
│   │   ├── components/
│   │   └── sort/
│   ├── services/              # Core services
│   │   ├── base.service.ts    # HTTP client base class
│   │   ├── util.service.ts    # Utility functions
│   │   └── preload.service.ts
│   └── store/                 # Global state management
│       ├── auth.store.ts      # Authentication state
│       └── job.store.ts       # Job-related state
├── hooks/                     # Custom React hooks
│   └── useAddJobValidation.ts
├── pages/                     # Application pages and routing
│   ├── Pages.tsx              # Main router component
│   ├── public/                # Public (unauthenticated) pages
│   │   ├── components/
│   │   │   ├── login/         # Login and authentication
│   │   │   │   ├── Login.tsx
│   │   │   │   ├── TotpModal.tsx
│   │   │   │   └── SecurityAvailabilityModal.tsx
│   │   │   ├── password-setup/
│   │   │   └── recovery-password/
│   │   ├── models/            # Public page data models
│   │   ├── services/          # Public API services
│   │   └── public.routes.tsx  # Public routing configuration
│   └── private/               # Private (authenticated) pages
│       ├── Layout.tsx         # Main application layout
│       ├── modules/           # Feature modules
│       │   ├── dashboard/     # Dashboard and analytics
│       │   ├── job/           # Job management
│       │   │   ├── components/
│       │   │   ├── models/
│       │   │   └── services/
│       │   ├── job-application/ # Application management
│       │   ├── candidate/     # Candidate profiles
│       │   ├── company/       # Company and user management
│       │   ├── profile/       # User profile management
│       │   └── steps/         # Onboarding wizard
│       ├── private.routes.tsx # Private routing configuration
│       └── util.ts           # Private utilities
└── index.tsx                 # Application entry point
```

## 🔧 How to Build and Run Locally

### Prerequisites
- **Node.js** (version 16.x or higher)
- **npm** (version 8.x or higher)
- **Backend API** running on configured endpoint
- **Keycloak** instance for authentication

### Environment Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd jobs-admin-console
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Environment Configuration**
   Create a `.env` file in the root directory:
   ```env
   REACT_APP_API_URL=http://localhost:8082
   REACT_APP_ROUTE_PREFIX=/admin
   ```

### Development Commands

- **Start development server**
  ```bash
  npm start
  # Runs on http://localhost:3000 by default
  # Use PORT=3001 npm start for custom port
  ```

- **Build for production**
  ```bash
  npm run build
  # Creates optimized build in ./build directory
  ```

- **Run tests**
  ```bash
  npm test
  # Runs test suite in interactive watch mode
  ```

- **Format code**
  ```bash
  npm run format
  # Formats code using Prettier with Tailwind plugin
  ```

### Production Deployment

1. **Build the application**
   ```bash
   npm run build
   ```

2. **Deploy build folder**
   - The `build` folder contains static files ready for deployment
   - Can be served by any static file server (Nginx, Apache, etc.)
   - Configure server to handle client-side routing (fallback to index.html)

## 🏛️ Component Hierarchy

### Application Architecture

```
App (Pages.tsx)
├── Router (HashRouter)
├── AuthHandler (Global auth state management)
└── Routes
    ├── PublicRoutes (/)
    │   ├── Login
    │   │   ├── SecurityAvailabilityModal
    │   │   └── TotpModal
    │   ├── PasswordSetup
    │   ├── RecoveryPassword
    │   └── OtpVerification
    └── PrivateRoutes (/admin/*)
        ├── Guard (Authentication protection)
        └── Layout (Main application shell)
            ├── Header (Navigation, user menu)
            ├── Sidebar (Module navigation)
            └── Content (Module-specific content)
                ├── Dashboard
                ├── Job Management
                │   ├── JobTable
                │   ├── JobForm
                │   └── JobPreview
                ├── Job Applications
                │   ├── JobApplicationTable
                │   └── JobApplicationForm
                ├── Candidates
                │   ├── CandidatesTable
                │   └── CandidateProfile
                ├── Company Management
                │   ├── CompanyProfile
                │   ├── UsersTable
                │   ├── ClientsTable
                │   └── StageScreen
                └── Profile
                    ├── MyProfile
                    └── ChangePassword
```

### Core Components

#### Authentication Flow
- **AuthHandler**: Manages global authentication state and token refresh
- **PrivateGuard**: Protects authenticated routes, redirects to login if needed
- **Login**: Main authentication component with 2FA support
- **TotpModal**: Two-factor authentication code input
- **SecurityAvailabilityModal**: Prompts users to enable 2FA security

#### Layout Components
- **Layout**: Main application shell with responsive sidebar and header
- **Header**: Top navigation with user profile dropdown and notifications
- **Sidebar**: Collapsible navigation menu with role-based visibility

#### Data Management
- **BaseService**: HTTP client with authentication, error handling, and loading states
- **AuthStore**: Encrypted persistent authentication state using Zustand
- **JobStore**: Job-related state management

#### Reusable UI Components
- **Table**: Enhanced data tables with sorting, filtering, and pagination
- **Button**: Consistent button styling with loading states
- **Input**: Form inputs with validation and error display
- **Select**: Enhanced select components with search and multi-select
- **Quill**: Rich text editor for job descriptions and content

### State Management Pattern

The application uses a hybrid state management approach:

1. **Global State (Zustand)**
   - Authentication state with encrypted persistence
   - Job-related data and filters
   - User preferences and settings

2. **Component State (React Hooks)**
   - Form data and validation
   - UI state (modals, loading, etc.)
   - Local component interactions

3. **Server State**
   - API data fetching through BaseService
   - Automatic error handling and loading states
   - Token-based authentication with auto-refresh

### Security Features

- **Encrypted Local Storage**: Sensitive data encrypted using CryptoJS
- **JWT Authentication**: Token-based auth with automatic refresh
- **Route Protection**: Private routes protected by authentication guards
- **2FA Support**: TOTP-based two-factor authentication
- **Session Management**: Automatic logout on token expiration
- **CSRF Protection**: Secure API communication patterns

## 🔗 Integration Points

### Backend API
- **Base URL**: Configurable via `REACT_APP_API_URL`
- **Authentication**: Bearer token (JWT) based
- **Error Handling**: Centralized error management with user-friendly messages

### Keycloak Integration
- **OAuth2 Flow**: Authorization code flow for secure authentication
- **2FA Setup**: Integration with Keycloak's TOTP configuration
- **User Management**: Profile and password management through Keycloak

### External Services
- **File Upload**: Support for resume and document uploads
- **Email Integration**: Password recovery and notifications
- **Analytics**: Job posting and application metrics

## 🚦 Development Guidelines

### Code Style
- **TypeScript**: Strict typing enabled for better code quality
- **Prettier**: Automatic code formatting with Tailwind CSS plugin
- **ESLint**: Code linting with React and TypeScript rules
- **Husky**: Pre-commit hooks for code quality enforcement

### Component Patterns
- **Functional Components**: Using React hooks for state management
- **Custom Hooks**: Reusable logic extraction
- **Context Providers**: Feature-specific state management
- **Error Boundaries**: Graceful error handling in component trees

### Testing Strategy
- **Unit Tests**: Component and utility function testing
- **Integration Tests**: API service and state management testing
- **E2E Tests**: Critical user flow validation

---

For more information about specific modules or components, refer to the inline documentation within each file.