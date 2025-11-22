# Food-View - Food Content Sharing Platform

A full-stack web application for sharing food content with a reel-based feed, similar to Instagram Reels but focused on food videos. Users can explore food videos from food partners, like, save, and interact with content.

## Project Overview

Food-View is a content-sharing platform where:
- **Regular Users** can browse, like, save, and watch food video reels
- **Food Partners** can upload and manage their food content
- **Core Features** include user authentication, video feeds, social interactions (likes/saves), and user profiles

## Tech Stack

### Frontend
- **React 19** - Modern UI framework with React Router for navigation
- **Vite** - Fast build tool with HMR (Hot Module Replacement)
- **Axios** - HTTP client for API communication
- **React Router DOM** - Client-side routing

### Backend
- **Express 5** - Node.js web framework
- **MongoDB + Mongoose** - NoSQL database with ODM
- **JWT** - JSON Web Token authentication
- **bcryptjs** - Password hashing and security
- **ImageKit** - Image/video storage and optimization
- **Multer** - File upload handling
- **CORS** - Cross-origin request handling

## Project Structure

```
food-view/
├── backend/                    # Express.js API server
│   ├── src/
│   │   ├── app.js             # Express app setup
│   │   ├── server.js          # Entry point
│   │   ├── controllers/       # Business logic
│   │   ├── routes/            # API endpoints
│   │   ├── models/            # MongoDB schemas
│   │   ├── middlewares/       # Auth & validation
│   │   ├── db/                # Database connection
│   │   └── services/          # Utility services
│   └── package.json
│
└── frontend/                   # React + Vite app
    ├── src/
    │   ├── pages/             # Page components
    │   │   ├── auth/          # Login/Register pages
    │   │   ├── food-partner/  # Partner-only pages
    │   │   └── general/       # Public pages
    │   ├── components/        # Reusable components
    │   ├── routes/            # Route definitions
    │   ├── styles/            # CSS stylesheets
    │   └── App.jsx
    └── package.json
```

## Features

### Authentication
- User registration & login
- Food Partner registration & login
- JWT-based authentication
- Password hashing with bcryptjs
- Separate auth endpoints for users and food partners

### User Features
- Browse food video reels (infinite feed)
- Like/unlike food videos
- Save/unsave videos for later
- View saved food content
- Food partner profiles

### Food Partner Features
- Upload and create food content (videos)
- Manage their own food videos
- View profile and analytics
- Track likes and saves on their content

### API Endpoints

**Authentication**
- `POST /api/auth/user/register` - Register regular user
- `POST /api/auth/user/login` - Login regular user
- `GET /api/auth/user/logout` - Logout user
- `POST /api/auth/food-partner/register` - Register food partner
- `POST /api/auth/food-partner/login` - Login food partner
- `GET /api/auth/food-partner/logout` - Logout food partner

**Food Content**
- `POST /api/food/` - Create food video (protected, food partners only)
- `GET /api/food/` - Get all food videos (protected, users only)
- `POST /api/food/like` - Like a food video (protected)
- `POST /api/food/save` - Save a food video (protected)
- `GET /api/food/save` - Get saved food videos (protected)

## Getting Started

### Prerequisites
- Node.js (v14+)
- MongoDB Atlas account (or local MongoDB)
- ImageKit account for media hosting

### Backend Setup

1. Install dependencies:
```bash
cd backend
npm install
```

2. Create `.env` file in backend directory:
```env
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_secret_key
IMAGEKIT_PUBLIC_KEY=your_imagekit_public_key
IMAGEKIT_PRIVATE_KEY=your_imagekit_private_key
IMAGEKIT_URL_ENDPOINT=your_imagekit_url
PORT=5000
```

3. Start the backend server:
```bash
npm start
```
The server runs on `http://localhost:5000`

### Frontend Setup

1. Install dependencies:
```bash
cd frontend
npm install
```

2. Start the development server:
```bash
npm run dev
```
The app runs on `http://localhost:5173`

3. Build for production:
```bash
npm run build
```

4. Preview production build:
```bash
npm run preview
```

## Usage

### As a Regular User
1. Go to `/register` and choose "User"
2. Register with email and password
3. Login to browse food reels
4. Like, save, and interact with food content
5. View saved videos in the `/saved` page

### As a Food Partner
1. Go to `/register` and choose "Food Partner"
2. Register with your business details
3. Login and navigate to `/create-food`
4. Upload food videos with description
5. View your profile at `/food-partner/:id`

## Database Models

**User** - Regular users who consume content
**FoodPartner** - Content creators/restaurants
**Food** - Video content with metadata
**Likes** - Track user likes on food videos
**Saves** - Track user saved videos

## Development

### ESLint
Run linting to check code quality:
```bash
cd frontend
npm run lint
```

### HMR (Hot Module Replacement)
The development server supports HMR - changes are reflected instantly without full page reload.

## API Documentation

Base URL: `http://localhost:5000/api`

All protected endpoints require a valid JWT token in cookies for authentication.

## File Upload
- Videos are uploaded via multipart form data
- Handled by Multer middleware
- Stored in memory then uploaded to ImageKit for optimization
