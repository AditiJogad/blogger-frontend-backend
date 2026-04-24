Blogger Platform
A full-stack blogging platform with a professional admin dashboard, JWT authentication, MongoDB Atlas support, and modular backend architecture using Node.js, Express, and Mongoose.

Highlights
Professional admin UI for posts, comments, authors, and categories
JWT-based authentication with bcrypt password hashing
MongoDB + Mongoose backend with validation, services, middleware, and modular routing
Comment moderation workflow with active, pending, and rejected states
React + Vite frontend connected to the existing backend routes
Ready for GitHub presentation with screenshot support
Submission Checklist
Use this project as a single GitHub repository containing both the frontend/ and backend/ folders.

Upload the complete blogger-front-back-end project code to your GitHub repository.
Add your repository URL in the included document file: Blogger-Aditi Jogad.doc.
If you keep frontend and backend in one repository, use the same GitHub URL for both entries in the document.
Upload the completed document file in classroom.
Important:

.gitignore is included so node_modules, frontend/dist, and backend/.env are not pushed accidentally.
Use backend/.env.example as the template for your local backend/.env.
Screenshots
Authentication Screen
Authentication Screen

Dashboard Overview
Dashboard Overview

Posts Management
Posts Management

Comments Management
Comments Management

Authors Management
Authors Management

Categories Management
Categories Management

Tech Stack
Frontend
React
Vite
Lucide React
CSS
Backend
Node.js
Express
MongoDB Atlas / MongoDB
Mongoose
JWT
bcrypt
cookie-parser
cors
helmet
Project Structure
backend/
  app.js
  index.js
  server.js
  config/
    database.js
    env.js
  constants/
    status.constants.js
  controllers/
    Auther-controller.js
    category-controller.js
    comments-controller.js
    post-controller.js
    users-controller.js
  helper/
    mongoose.js
  helpers/
    auth.js
  middlewares/
    auth.middleware.js
    error.middleware.js
    validate.middleware.js
  model/
    comment-model.js
    user-model.js
  models/
    auther.js
    category.js
    comment.js
    posts.js
    users.js
  routers/
    Auther.js
    category.js
    comments.js
    post.js
    users.js
  routes/
    index.js
  schemas/
    auther-schema.js
    category-schema.js
    comment-schema.js
    posts-schema.js
    users-schema.js
  services/
    auth.service.js
    comment.service.js
  utils/
    api-error.js
    async-handler.js
    jwt.js
  validators/
    auth.validator.js
    comment.validator.js
    common.validator.js
frontend/
  index.html
  package.json
  src/
    main.jsx
    styles.css
screenshots/
requirements.txt
docker-compose.yml
Architecture
Separated app bootstrapping into app.js and server.js
Added environment and database config with Atlas-friendly setup
Added centralized middleware for auth, validation, and error handling
Added services layer for cleaner business logic
Rebuilt the comments module with validation, indexing, timestamps, static and instance methods
Replaced weak password storage with bcrypt hashing
Added a clean React/Vite admin dashboard
Added root install scripts and Docker support for local MongoDB
Comments Module
The comments module includes:

comment: required, trimmed, minimum 3 characters
subject: required, trimmed
status: enum active, pending, rejected
post_id: required ObjectId, indexed, ref to Posts
created: default Date.now
createdAt and updatedAt timestamps
compound index on { post_id: 1, createdAt: -1 }
static method getCommentsByPost(postId)
instance method approveComment()
pre-save sanitization and empty-value protection
API Examples
Login:

curl -X POST http://localhost:3000/users/login \
  -H "Content-Type: application/json" \
  -d "{\"email\":\"admin@example.com\",\"password\":\"Admin@123\"}"
Create comment:

curl -X POST http://localhost:3000/comment/addcomment \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <token>" \
  -d "{\"subject\":\"Nice post\",\"comment\":\"This article helped me.\",\"post_id\":\"66291a4bc7f2f6799e721111\"}"
Get comments by post:

curl http://localhost:3000/comment/post/66291a4bc7f2f6799e721111 \
  -H "Authorization: Bearer <token>"
Update comment status:

curl -X PUT http://localhost:3000/comment/updatecomment/66291a4bc7f2f6799e722222 \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <token>" \
  -d "{\"status\":\"active\"}"
Delete comment:

curl -X DELETE http://localhost:3000/comment/deletecomment/66291a4bc7f2f6799e722222 \
  -H "Authorization: Bearer <token>"
Run Locally
Backend
cd backend
npm install
npm start
Frontend
cd frontend
npm install
npm start
Frontend runs on:

http://localhost:3001
Backend runs on:

http://localhost:3000
Root Scripts
From the project root:

npm run install:all
npm run frontend
npm start
Optional local MongoDB with Docker:

npm run db:up
Environment
Use backend/.env.example as the template for backend/.env.

If you use MongoDB Atlas, set:

MONGODB_URI=mongodb+srv://<username>:<password>@<cluster>/<database>?appName=Cluster0
Notes
If you see connect ECONNREFUSED 127.0.0.1:27017, MongoDB is not running locally.
If you see EADDRINUSE: address already in use :::3000, another backend server is already running on port 3000.
In PowerShell, prefer Invoke-RestMethod or curl.exe instead of plain curl.
This workspace is not currently connected to a GitHub remote, so you still need to initialize or link a repository before pushing.
