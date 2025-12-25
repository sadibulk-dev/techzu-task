# Techzu Task - Comment System

A full-stack comment system with real-time updates, user authentication, and modern UI.

## Features

- **User Authentication**: Register and login with JWT-based authentication
- **Real-time Comments**: Live comment updates using Socket.io
- **Comment Management**: Create, reply to, sort, and paginate comments
- **Responsive Design**: Modern UI built with React and SCSS
- **API Security**: Rate limiting, CORS, Helmet for security
- **Type Safety**: TypeScript for frontend type checking

## Tech Stack

### Backend
- Node.js with Express.js
- MongoDB with Mongoose
- Socket.io for real-time communication
- JWT (JSON Web Tokens) for authentication
- bcryptjs for password hashing
- Express Validator for input validation
- Helmet for security headers
- Express Rate Limiter

### Frontend
- React 19 with TypeScript
- React Router for navigation
- Socket.io Client for real-time updates
- Axios for API requests
- SCSS for styling
- React Icons

## Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v14 or higher) - [Download Node.js](https://nodejs.org/)
- **MongoDB** (v4.4 or higher) - [Download MongoDB](https://www.mongodb.com/try/download/community)
- **npm** (comes with Node.js) or **yarn** - [Install Yarn](https://yarnpkg.com/getting-started/install)
- **Git** - [Download Git](https://git-scm.com/downloads)

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/sadibulk-dev/techzu-task.git
cd techzu-task
```

### 2. Backend Setup

Navigate to the backend directory and install dependencies:

```bash
cd backend
npm install
```

Create a `.env` file in the `backend` directory and copy the contents from `.env.example`:

```bash
cp .env.example .env
```

Update the `.env` file with your configuration:

```env
# Server Configuration
PORT=5000
NODE_ENV=development

# MongoDB Configuration
MONGODB_URI=mongodb://localhost:27017/comment-system

# JWT Configuration
JWT_SECRET=your-super-secret-jwt-key-change-this-in-production
JWT_EXPIRE=7d

# CORS Configuration
CLIENT_URL=http://localhost:3000

# Rate Limiting
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=100
```

**Important**: Change the `JWT_SECRET` to a strong, unique value in production.

### 3. Frontend Setup

Navigate to the frontend directory and install dependencies:

```bash
cd ../frontend
npm install
```

Create a `.env` file in the `frontend` directory and copy the contents from `.env.example`:

```bash
cp .env.example .env
```

The frontend `.env` file should contain:

```env
# API Configuration
REACT_APP_API_URL=http://localhost:5000/api

# Socket.io Configuration
REACT_APP_SOCKET_URL=http://localhost:5000

# Environment
NODE_ENV=development
```

### 4. MongoDB Setup

Make sure MongoDB is running on your system.

**Windows:**
- If installed as a service, MongoDB starts automatically
- Otherwise, run: `mongod`

**Mac/Linux:**
```bash
# Using Homebrew
brew services start mongodb-community

# Or manually
mongod --dbpath /path/to/your/data/directory
```

Verify MongoDB is running on `localhost:27017`.

## Running the Application

### Option 1: Run Backend and Frontend Separately

**Terminal 1 - Backend:**
```bash
cd backend
npm run dev
```
The backend server will start on `http://localhost:5000`

**Terminal 2 - Frontend:**
```bash
cd frontend
npm start
```
The frontend application will open on `http://localhost:3000`

### Option 2: Run Both Simultaneously (Recommended)

From the root directory, you can run both servers using two terminals:

**Terminal 1 - Backend:**
```bash
cd backend
npm run dev
```

**Terminal 2 - Frontend:**
```bash
cd frontend
npm start
```

Or use concurrently (if you want to add this script to root package.json):

```bash
npm install concurrently --save-dev
```

Then add to root `package.json`:
```json
"scripts": {
  "dev": "concurrently \"npm run backend\" \"npm run frontend\"",
  "backend": "cd backend && npm run dev",
  "frontend": "cd frontend && npm start"
}
```

## Usage

1. **Open your browser** and navigate to `http://localhost:3000`

2. **Register a new account**:
   - Click on the "Register" link
   - Fill in your email, username, and password
   - Submit the form

3. **Login** with your credentials

4. **Create comments**:
   - Navigate to the comments section
   - Type your comment in the comment form
   - Click "Post Comment"

5. **Reply to comments**:
   - Click on a comment to expand it
   - Use the reply form to respond

6. **Sort comments**:
   - Use the sort dropdown to order by: Newest, Oldest, Most Likes

7. **Paginate**:
   - Use the pagination controls to navigate through comments

## Project Structure

```
techzu-task/
├── backend/
│   ├── config/
│   │   └── database.js          # MongoDB connection configuration
│   ├── controllers/
│   │   ├── authController.js    # Authentication logic
│   │   └── commentController.js # Comment CRUD operations
│   ├── middleware/
│   │   ├── auth.js              # JWT authentication middleware
│   │   └── errorHandler.js      # Error handling middleware
│   ├── models/
│   │   ├── Comment.js           # Comment mongoose model
│   │   └── User.js              # User mongoose model
│   ├── routes/
│   │   ├── auth.js              # Authentication routes
│   │   └── comments.js          # Comment routes
│   ├── utils/
│   │   └── validation.js        # Input validation utilities
│   ├── .env                     # Backend environment variables
│   ├── .env.example             # Environment variables template
│   ├── package.json             # Backend dependencies
│   └── server.js                # Entry point
├── frontend/
│   ├── public/                  # Static files
│   ├── src/
│   │   ├── components/
│   │   │   ├── Auth/            # Authentication components
│   │   │   │   ├── Login.tsx
│   │   │   │   ├── Register.tsx
│   │   │   │   └── Auth.scss
│   │   │   ├── Comments/        # Comment components
│   │   │   │   ├── CommentForm.tsx
│   │   │   │   ├── CommentItem.tsx
│   │   │   │   ├── CommentList.tsx
│   │   │   │   ├── EnhancedPagination.tsx
│   │   │   │   ├── Pagination.tsx
│   │   │   │   ├── ReplyForm.tsx
│   │   │   │   ├── SortOptions.tsx
│   │   │   │   └── Comments.scss
│   │   │   ├── Layout.tsx      # Main layout component
│   │   │   └── ProtectedRoute.tsx # Route protection
│   │   ├── context/
│   │   │   └── AuthContext.tsx  # Authentication context
│   │   ├── services/
│   │   │   ├── api.ts           # API service with axios
│   │   │   └── socket.ts        # Socket.io client
│   │   ├── types/
│   │   │   └── index.d.ts       # TypeScript type definitions
│   │   ├── utils/
│   │   │   └── formatCount.ts   # Utility functions
│   │   ├── App.tsx              # Main App component
│   │   ├── App.scss             # App styles
│   │   ├── index.tsx            # Entry point
│   │   └── global.d.ts          # Global type declarations
│   ├── .env                     # Frontend environment variables
│   ├── .env.example             # Environment variables template
│   ├── package.json             # Frontend dependencies
│   └── tsconfig.json            # TypeScript configuration
└── README.md                    # This file
```

## API Endpoints

### Authentication

- `POST /api/auth/register` - Register a new user
- `POST /api/auth/login` - Login a user
- `GET /api/auth/me` - Get current user (protected)

### Comments

- `GET /api/comments` - Get all comments with pagination
- `POST /api/comments` - Create a new comment (protected)
- `POST /api/comments/:id/replies` - Reply to a comment (protected)
- `PUT /api/comments/:id/like` - Like/unlike a comment (protected)
- `DELETE /api/comments/:id` - Delete a comment (protected)

## Real-time Events

The application uses Socket.io for real-time updates:

- `newComment` - Emitted when a new comment is created
- `newReply` - Emitted when a new reply is added
- `commentDeleted` - Emitted when a comment is deleted
- `commentLiked` - Emitted when a comment is liked/unliked

## Troubleshooting

### MongoDB Connection Issues

If you can't connect to MongoDB:

1. Verify MongoDB is running:
   ```bash
   # On Windows
   net start MongoDB

   # On Mac/Linux
   brew services list
   ```

2. Check your MongoDB URI in `backend/.env`

3. Ensure MongoDB is listening on port 27017

### Port Already in Use

If you get a "port already in use" error:

**Windows:**
```bash
netstat -ano | findstr :5000
taskkill /PID <PID> /F
```

**Mac/Linux:**
```bash
lsof -ti:5000 | xargs kill -9
```

### CORS Errors

If you encounter CORS errors:

1. Verify `CLIENT_URL` in `backend/.env` matches your frontend URL
2. Check that the frontend is running on port 3000
3. Ensure no browser extensions are interfering

### Socket.io Connection Issues

If real-time features aren't working:

1. Verify both backend and frontend are running
2. Check browser console for connection errors
3. Verify `REACT_APP_SOCKET_URL` in `frontend/.env`

### Environment Variables Not Loading

If environment variables aren't being recognized:

1. Ensure `.env` files exist in both `backend/` and `frontend/` directories
2. Restart the servers after creating/modifying `.env` files
3. Frontend variables must start with `REACT_APP_`

## Development Scripts

### Backend

- `npm start` - Start production server
- `npm run dev` - Start development server with nodemon

### Frontend

- `npm start` - Start development server
- `npm run build` - Build for production
- `npm test` - Run tests

## Production Deployment

For production deployment:

1. Set `NODE_ENV=production` in both `.env` files
2. Use a strong `JWT_SECRET`
3. Use a production MongoDB instance (e.g., MongoDB Atlas)
4. Build the frontend: `npm run build` in the frontend directory
5. Use a process manager like PM2 for the backend
6. Configure proper SSL/HTTPS
7. Set up proper CORS origins

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the ISC License.

## Support

If you encounter any issues or have questions, please open an issue on the GitHub repository.

---

**Happy Coding! 🚀**
