# Personal Information

**Name: Md Toushif Alam**

**University: IIT Dhanbad**

**Department: Electronics and Communication Engineering**


# System Design Document

## 1. Introduction

The Real-Time Messaging Web Application allows users to communicate with each other through private and group chats. The app supports real-time updates using WebSockets, user authentication, and message history management.

## 2. Features

- **User Authentication**: Users can register, log in, and manage their accounts.
- **Messaging**: Users can send and receive messages in real-time.
- **Group Chat**: Multiple users can join a group chat and communicate.
- **Real-time Updates**: Messages are instantly updated using **Socket.IO**.
- **Responsive UI**: The interface is designed for ease of use with clear and intuitive interactions.

## 3. Tech Stack

### Frontend:
- **ReactJS**: For building the user interface.
- **Socket.IO (Client)**: To handle real-time communication with the backend.
- **Axios**: For making HTTP requests to the backend.
- **Chakra UI**: For styling components and creating a clean, responsive design.

### Backend:
- **Node.js**: Backend runtime to serve APIs.
- **Express.js**: Web framework to create RESTful APIs.
- **MongoDB (NoSQL Database)**: Stores user information, chat rooms, and message history.
- **Socket.IO (Server)**: Manages real-time communication between clients and the server.

### Deployment:
- **Render**: The application is deployed on Render for hosting.
- **MongoDB Atlas**: The cloud database for storing application data.

## 4. Architecture Overview

This is a high-level overview of the architecture:

- **User (Client)**: Interacts with the web app using a browser.
- **Frontend (ReactJS)**: Handles UI rendering, API requests, and real-time updates.
- **Backend (Node.js + Express)**: Provides REST APIs for user management, chat functionalities, and real-time communication using Socket.IO.
- **Database (MongoDB)**: Stores user data, chat data, and messages.
- **Socket.IO**: Enables real-time communication between clients and the server.
- **Render**: Hosts both the frontend and backend services, and MongoDB Atlas hosts the database.

### Architecture Diagram

![Architecture Diagram](./docs/SystemDesignImage.png)

- **Users** interact with the frontend (ReactJS) via HTTP requests and WebSocket connections.
- **Frontend (ReactJS)** communicates with the **Backend (Node.js)** using API requests for authentication, chat messages, and uses **Socket.IO** for real-time updates.
- **Backend (Node.js)** interacts with **MongoDB** to store and retrieve user and chat data, and sends real-time updates to the clients using **Socket.IO**.
- **MongoDB (Database)** holds the persistent data, including user information, chats, and message history.
  
## 5. API Overview

### 1. User API
- **POST /api/user/register**: Register a new user.
- **POST /api/user/login**: Log in a user.

### 2. Chat API
- **GET /api/chat**: Get all chats of the logged-in user.
- **POST /api/chat**: Create a new chat or group.

### 3. Message API
- **GET /api/message/:chatId**: Get messages of a specific chat.
- **POST /api/message**: Send a new message.

## 6. Real-Time Communication with Socket.IO

**Socket.IO** is used for bi-directional real-time communication. When a user sends a message:
- The **Frontend** emits the message event to the **Backend**.
- The **Backend** processes the message and emits it to all users in the chat via **Socket.IO**.

### Key Events:
- **setup**: Set up the socket connection for a user.
- **join chat**: User joins a specific chat room.
- **new message**: Broadcasts the new message to users in the same chat room.

## 7. Database Design

### Collections:
1. **Users**:
   - _id
   - name
   - email
   - password (hashed)
   - profile picture (optional)

2. **Chats**:
   - _id
   - chatName
   - isGroupChat (boolean)
   - users (array of user IDs)
   - latestMessage (reference to the last message)

3. **Messages**:
   - _id
   - sender (reference to User)
   - content (message text)
   - chat (reference to Chat)
   - timestamp

## 8. Security Considerations

- **Password Encryption**: User passwords are stored securely using **bcrypt**.
- **JWT Authentication**: Each user is authenticated using a **JWT token** that is validated with every API request.
- **CORS**: Configured to allow requests from specific origins (React app hosted on Render).
  
## 9. Conclusion

This system leverages modern web technologies like **ReactJS**, **Node.js**, and **Socket.IO** to provide a seamless, real-time messaging experience. MongoDB serves as the database for persistent storage, while the app is deployed and hosted on **Render** and **MongoDB Atlas**, ensuring scalability and reliability.

