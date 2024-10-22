
# **Leaderboard Backend**

This is the backend for the Leaderboard application built using **Node.js** with **Express** and **MongoDB**. The backend handles user management, point claiming, and real-time updates for the leaderboard using **Socket.io**.

## **Features**
- API for user management (adding, fetching users).
- API to claim points for users, updating their scores.
- Real-time leaderboard updates for all connected clients.
- Mongoose models for MongoDB schemas.

## **Technologies Used**
- **Node.js**
- **Express**
- **Socket.io**
- **Mongoose** (for MongoDB interactions)

## **Installation**

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/leaderboard-backend.git
cd leaderboard-backend
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Set Up Environment Variables

Create a `.env` file in the root directory of the project with the following content:

```bash
# MongoDB connection URI
MONGODB_URI=mongodb://localhost:27017/leaderboard

# Port on which the backend will run
PORT=3000
```

Make sure to replace `mongodb://localhost:27017/leaderboard` with your actual MongoDB connection string if using a remote MongoDB instance.

### 4. Start MongoDB (if running locally)

If you’re using MongoDB locally, ensure that it is running:

```bash
mongod
```

### 5. Start the Backend Server

Once you've installed all the dependencies and MongoDB is running, start the backend server:

```bash
npm start
```

The server will run on `http://localhost:3000`.

## **Project Structure**

```
leaderboard-backend/
├── controllers/               # Contains business logic (user, claim points)
│   ├── userController.js      # Handles user-related logic
├── models/                    # Mongoose models
│   ├── User.js                # User schema
│   ├── ClaimHistory.js        # Claim history schema
├── routes/                    # API routes
│   ├── userRoutes.js          # User-related routes
├── socket.js                  # Socket.io setup and logic
├── index.js                   # Main entry point for the Express server
├── .env                       # Environment variables
├── package.json               # Node.js dependencies
└── README.md                  # Instructions and documentation for the project
```

### **Key Files**

- **`index.js`**: Main entry point of the application. It initializes the Express app, sets up middleware, connects to MongoDB, and starts the Socket.io server.
- **`controllers/userController.js`**: Contains functions for adding users, fetching users, and claiming points.
- **`models/User.js`**: Mongoose schema for the user data, including fields for username and total points.
- **`models/ClaimHistory.js`**: Mongoose schema for tracking the history of points claimed by users.
- **`routes/userRoutes.js`**: Defines API endpoints for user operations, such as adding users and claiming points.
- **`socket.js`**: Manages real-time connections and events with Socket.io, broadcasting updates to connected clients.

## **How It Works**

1. **API Endpoints**:
   - **POST /users**: Adds a new user to the database.
   - **GET /users**: Fetches all users from the database.
   - **POST /users/:id/claim**: Claims random points for a user specified by their ID.

2. **Real-Time Functionality**:
   - The backend uses **Socket.io** to establish a WebSocket connection with clients.
   - When points are claimed, the backend broadcasts the updated leaderboard to all connected clients, ensuring everyone sees the latest scores in real time.

3. **Mongoose Models**:
   - **User**: Represents a user in the leaderboard with fields for the username and total points.
   - **ClaimHistory**: Tracks each claim event, storing the user ID and points claimed.

## **Usage**

After starting the backend server, you can interact with the API using tools like **Postman** or directly through your frontend application. Here are some example requests:

### Add a User
```http
POST /users
Content-Type: application/json

{
    "username": "JohnDoe"
}
```

### Fetch Users
```http
GET /users
```

### Claim Points for a User
```http
POST /users/:id/claim
```

## **Troubleshooting**

### Common Issues:

1. **MongoDB Connection Error**: 
   - Ensure MongoDB is running locally or check the connection URI in the `.env` file.

2. **CORS Issues**: 
   - If you're accessing the API from a different domain (like your frontend), ensure CORS is properly configured.

3. **500 Internal Server Error**: 
   - Check server logs for details on any unexpected errors. Ensure all expected fields are being provided in requests.

### Logs:
- All server activity, including errors and connections, will be logged in the terminal where the backend server is running.

## **Future Improvements**
- Implement user authentication for added security.
- Add a more robust error handling mechanism.
- Introduce a system for tracking user activities and statistics.

