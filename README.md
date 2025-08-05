# FileShare - Secure File Sharing Platform

A modern, secure file sharing platform built with Next.js, NestJS, and Appwrite. Share files with expirable links, track downloads, and manage your uploads with a beautiful, responsive interface.

![FileShare Architecture](https://img.shields.io/badge/Architecture-Three--Tier-blue)
![Frontend](https://img.shields.io/badge/Frontend-Next.js%2014-black)
![Backend](https://img.shields.io/badge/Backend-NestJS-red)
![Database](https://img.shields.io/badge/Database-Appwrite-pink)
![Auth](https://img.shields.io/badge/Auth-JWT-green)

## 🚀 Features

### 🔐 **Authentication & Security**
- JWT-based authentication with secure token management
- User registration and login with email verification
- Protected routes and API endpoints
- Session management with automatic token refresh

### 📁 **File Management**
- Drag & drop file upload with progress indicators
- Support for all file types and sizes
- File metadata storage and management
- User-specific file organization
- File deletion with cascade cleanup

### 🔗 **Secure Sharing**
- Generate unique, secure share links
- Configurable expiration dates
- Download count tracking and limits
- Public access without authentication required
- Share link management and revocation

### 🎨 **User Interface**
- Modern, responsive design that works on all devices
- Dark/Light theme support
- Intuitive drag & drop interface
- Real-time upload progress
- Beautiful file management dashboard

## 🏗️ Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Next.js       │    │   Next.js       │    │   NestJS        │
│   Frontend      │───▶│   API Routes    │───▶│   Backend       │
│   (Port 3000)   │    │   (Middleware)  │    │   (Port 8000)   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                                        │
                                               ┌─────────────────┐
                                               │   Appwrite      │
                                               │   Database &    │
                                               │   Storage       │
                                               └─────────────────┘
```

### **Three-Tier Architecture:**
1. **Frontend Layer**: Next.js React application with TypeScript
2. **API Layer**: Next.js API routes acting as middleware
3. **Backend Layer**: NestJS application with Appwrite integration

## 🛠️ Tech Stack

### **Frontend**
- **Next.js 14** - React framework with App Router
- **TypeScript** - Type-safe JavaScript
- **Tailwind CSS** - Utility-first CSS framework
- **React Context** - State management
- **Fetch API** - HTTP client

### **Backend**
- **NestJS** - Progressive Node.js framework
- **TypeScript** - Type-safe server-side development
- **JWT** - JSON Web Token authentication
- **Passport** - Authentication middleware
- **Multer** - File upload handling

### **Database & Storage**
- **Appwrite** - Backend-as-a-Service platform
- **Appwrite Database** - Document-based database
- **Appwrite Storage** - File storage with CDN
- **Appwrite Auth** - User authentication service

## 📋 Prerequisites

- **Node.js** 18+ and npm
- **Appwrite** account and project setup
- **Git** for version control

## 🚀 Quick Start

### 1. Clone the Repository
```bash
git clone https://github.com/Amanbig/FileShare.git
cd FileShare
```

### 2. Set Up Appwrite Project

1. Create an [Appwrite](https://appwrite.io) account
2. Create a new project
3. Set up the following collections in your database:

**Users Collection (`users`):**
```json
{
  "user_id": "string",
  "email": "string", 
  "name": "string",
  "created_at": "datetime",
  "updated_at": "datetime"
}
```

**Files Collection (`files`):**
```json
{
  "fileId": "string",
  "originalName": "string",
  "size": "integer",
  "mimeType": "string", 
  "userId": "string",
  "createdAt": "datetime"
}
```

**Shares Collection (`shares`):**
```json
{
  "fileId": "string",
  "shareToken": "string",
  "downloadCount": "integer",
  "maxDownloads": "integer",
  "expiresAt": "datetime",
  "createdAt": "datetime"
}
```

4. Create a storage bucket for files
5. Get your project credentials

### 3. Configure Environment Variables

**Backend (`backend/.env`):**
```env
# Appwrite Configuration
APPWRITE_ENDPOINT=https://cloud.appwrite.io/v1
APPWRITE_PROJECT_ID=your_project_id
APPWRITE_API_KEY=your_api_key
APPWRITE_DATABASE_ID=your_database_id
APPWRITE_USER_COLLECTION_ID=users
APPWRITE_FILES_COLLECTION_ID=files
APPWRITE_SHARES_COLLECTION_ID=shares
APPWRITE_BUCKET_ID=your_bucket_id

# JWT Configuration
JWT_SECRET=your-super-secret-jwt-key-change-this-in-production
JWT_EXPIRES_IN=24h

# Application Configuration
BASE_URL=http://localhost:8000
PORT=8000
```

**Frontend (`frontend/.env.local`):**
```env
# Next.js Frontend Configuration
NEXT_PUBLIC_BACKEND_URL=/api

# NestJS Backend URL (for Next.js API routes to communicate with)
NESTJS_BACKEND_URL=http://localhost:8000
```

### 4. Install Dependencies

**Backend:**
```bash
cd backend
npm install
```

**Frontend:**
```bash
cd frontend
npm install
```

### 5. Start the Applications

**Start NestJS Backend (Terminal 1):**
```bash
cd backend
npm run start:dev
```

**Start Next.js Frontend (Terminal 2):**
```bash
cd frontend
npm run dev -- --port 3001
```

### 6. Access the Application

- **Main Application**: http://localhost:3000
- **Share Links**: http://localhost:3000/share/[token]
- **Backend API**: http://localhost:8000

## 📖 Usage

### **Getting Started**
1. Visit http://localhost:3000
2. Create an account or sign in
3. Upload files using drag & drop or file picker
4. Manage your files from the dashboard

### **Sharing Files**
1. Click the "Share" button on any file
2. Share link is automatically copied to clipboard
3. Set expiration dates and download limits (optional)
4. Share the link with anyone

### **Accessing Shared Files**
1. Open the shared link in any browser
2. View file information and download statistics
3. Download the file (if not expired or limit reached)

## 🔧 Development

### **Project Structure**
```
FileShare/
├── backend/                 # NestJS Backend
│   ├── src/
│   │   ├── auth/           # Authentication module
│   │   ├── files/          # File management module
│   │   ├── shares/         # Share management module
│   │   ├── appwrite/       # Appwrite integration
│   │   └── config/         # Configuration files
│   └── package.json
├── frontend/               # Next.js Frontend
│   ├── src/
│   │   ├── app/           # App Router pages
│   │   ├── components/    # React components
│   │   ├── contexts/      # React contexts
│   │   ├── lib/          # Utility functions
│   │   └── api/          # API route handlers
│   └── package.json
└── README.md
```

### **Available Scripts**

**Backend:**
- `npm run start:dev` - Start development server
- `npm run build` - Build for production
- `npm run start:prod` - Start production server
- `npm run test` - Run tests

**Frontend:**
- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run start` - Start production server
- `npm run lint` - Run ESLint

## 🔒 Security Features

- **JWT Authentication** - Secure token-based authentication
- **Route Protection** - Protected API endpoints and pages
- **File Ownership** - Users can only access their own files
- **Share Validation** - Expiration dates and download limits
- **Input Validation** - Server-side validation for all inputs
- **CORS Protection** - Configured for secure cross-origin requests

## 🚀 Deployment

### **Backend Deployment**
1. Build the application: `npm run build`
2. Set production environment variables
3. Deploy to your preferred platform (Heroku, DigitalOcean, AWS, etc.)

### **Frontend Deployment**
1. Build the application: `npm run build`
2. Set production environment variables
3. Deploy to Vercel, Netlify, or your preferred platform

### **Environment Variables for Production**
- Change `JWT_SECRET` to a strong, unique secret
- Update `BASE_URL` to your production domain
- Configure CORS settings for production domains
- Set up proper SSL certificates

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

If you encounter any issues or have questions:

1. Check the [Issues](../../issues) page
2. Create a new issue with detailed information
3. Include error messages and steps to reproduce

## 🙏 Acknowledgments

- [Next.js](https://nextjs.org/) - The React framework for production
- [NestJS](https://nestjs.com/) - A progressive Node.js framework
- [Appwrite](https://appwrite.io/) - Secure backend server for web & mobile apps
- [Tailwind CSS](https://tailwindcss.com/) - A utility-first CSS framework

---

[![Buy Me a Coffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-%E2%98%95%EF%B8%8F-orange?style=for-the-badge)](https://buymeacoffee.com/amanpreet)

**Built with ❤️ by the FileShare team**
