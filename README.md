# Real-Time Chat Application

A modern, production-ready real-time chat application built with microservices architecture, featuring instant messaging, online presence tracking, typing indicators, image sharing, and passwordless OTP-based authentication.

## 🌟 Project Overview

This full-stack chat application demonstrates enterprise-grade web development practices with a microservices backend and a responsive Next.js 15 frontend. Built with TypeScript throughout, it provides seamless real-time communication with features like message read receipts, online/offline status indicators, typing awareness, image sharing via Cloudinary, and secure JWT-based authentication.

## 🏗️ Architecture

The project follows a microservices architecture with three independent backend services:

- **User Service** (Port 5000): Handles authentication, user management, and OTP verification
- **Chat Service** (Port 5002): Manages real-time messaging, chat rooms, and WebSocket connections
- **Mail Service**: Processes email notifications asynchronously via RabbitMQ

### Technology Stack

**Frontend:**
- Next.js 15.3.4 with App Router (React 19)
- TypeScript for type safety
- Tailwind CSS 4 for styling
- Socket.IO Client 4.8.1 for real-time communication
- Axios 1.10.0 for HTTP requests
- React Context API for state management
- React Hot Toast for notifications
- Lucide React for icons
- js-cookie for cookie management
- Moment.js for date formatting

**Backend:**
- Node.js with Express.js
- TypeScript for type-safe development
- MongoDB with Mongoose (Database)
- Redis (OTP storage, caching & rate limiting)
- RabbitMQ (Message queue for async email processing)
- Socket.IO (WebSocket for real-time features)
- Cloudinary (Cloud-based image storage & CDN)
- JWT (Stateless authentication)
- Nodemailer (Email delivery)
- Multer (File upload handling)

## ✨ Key Features

### Authentication & Security
- **Passwordless OTP Authentication**: Secure 6-digit OTP sent via email
- **JWT Tokens**: Stateless authentication with 15-day cookie expiration
- **Rate Limiting**: Redis-based rate limiting to prevent OTP spam and abuse
- **Secure Image Upload**: Cloudinary integration with file validation
- **HTTP-only Cookies**: XSS protection for token storage
- **Input Sanitization**: Protection against injection attacks

### Real-Time Messaging
- **Instant Messaging**: WebSocket-based real-time message delivery with Socket.IO
- **Typing Indicators**: Live typing awareness with debounced events
- **Online/Offline Status**: Real-time presence tracking for all users
- **Message Read Receipts**: Single/double check marks for delivery and seen status
- **Image Sharing**: Upload, preview, and share images with Cloudinary CDN
- **Message Deduplication**: Prevents duplicate messages in UI
- **Auto-scroll**: Automatically scrolls to latest messages

### User Experience
- **Responsive Design**: Mobile-first approach that adapts to all screen sizes
- **Unseen Message Counter**: Real-time badge showing unread count per chat
- **Smart Chat Sorting**: Conversations automatically sorted by latest activity
- **User Search**: Find and start conversations with any registered user
- **Profile Management**: Update display name and view user information
- **Dark Theme**: Modern dark UI with glassmorphism effects
- **Loading States**: Visual feedback for all async operations
- **Toast Notifications**: User-friendly notifications for actions and errors
- **Keyboard Navigation**: Accessible keyboard shortcuts and focus management

## 📁 Project Structure

```
chat-application/
├── backend/
│   ├── chat/                          # Chat & messaging service (Port 5002)
│   │   ├── src/
│   │   │   ├── config/               # Configuration files
│   │   │   │   ├── cloudinary.ts     # Cloudinary setup
│   │   │   │   ├── db.ts             # MongoDB connection
│   │   │   │   ├── socket.ts         # Socket.IO setup
│   │   │   │   └── TryCatch.ts       # Error handling wrapper
│   │   │   ├── controllers/          # Request handlers
│   │   │   │   └── chat.ts           # Chat & message logic
│   │   │   ├── middlewares/          # Express middlewares
│   │   │   │   ├── isAuth.ts         # JWT authentication
│   │   │   │   └── multer.ts         # File upload handling
│   │   │   ├── models/               # MongoDB schemas
│   │   │   │   ├── Chat.ts           # Chat model
│   │   │   │   └── Messages.ts       # Message model
│   │   │   ├── routes/               # API routes
│   │   │   └── index.ts              # Server entry point
│   │   ├── .env                      # Environment variables
│   │   ├── package.json
│   │   └── tsconfig.json
│   │
│   ├── mail/                          # Email notification service (Port 5003)
│   │   ├── src/
│   │   │   ├── consumer.ts           # RabbitMQ consumer
│   │   │   └── index.ts              # Service entry point
│   │   ├── .env
│   │   ├── package.json
│   │   └── tsconfig.json
│   │
│   ├── user/                          # User authentication service (Port 5000)
│   │   ├── src/
│   │   │   ├── config/               # Configuration files
│   │   │   │   ├── db.ts             # MongoDB connection
│   │   │   │   ├── generateToken.ts  # JWT generation
│   │   │   │   ├── rabbitmq.ts       # RabbitMQ setup
│   │   │   │   └── TryCatch.ts       # Error handling
│   │   │   ├── controllers/          # Request handlers
│   │   │   │   └── user.ts           # User & auth logic
│   │   │   ├── middleware/           # Express middlewares
│   │   │   │   └── isAuth.ts         # JWT authentication
│   │   │   ├── model/                # MongoDB schemas
│   │   │   │   └── User.ts           # User model
│   │   │   ├── routes/               # API routes
│   │   │   └── index.ts              # Server entry point
│   │   ├── .env
│   │   ├── package.json
│   │   └── tsconfig.json
│   │
│   └── README.md                      # Backend documentation
│
├── frontend/                          # Next.js application (Port 3000)
│   ├── src/
│   │   ├── app/                      # Next.js App Router pages
│   │   │   ├── chat/                 # Main chat interface
│   │   │   │   └── page.tsx
│   │   │   ├── login/                # Login page
│   │   │   │   └── page.tsx
│   │   │   ├── profile/              # User profile page
│   │   │   │   └── page.tsx
│   │   │   ├── verify/               # OTP verification page
│   │   │   │   └── page.tsx
│   │   │   ├── layout.tsx            # Root layout
│   │   │   ├── page.tsx              # Home (redirects to chat)
│   │   │   └── globals.css           # Global styles
│   │   ├── components/               # Reusable React components
│   │   │   ├── ChatHeader.tsx        # Chat header with user info
│   │   │   ├── ChatMessages.tsx      # Message list display
│   │   │   ├── ChatSidebar.tsx       # Sidebar with chat list
│   │   │   ├── Loading.tsx           # Loading spinner
│   │   │   ├── MessageInput.tsx      # Message input with image upload
│   │   │   └── VerifyOtp.tsx         # OTP verification form
│   │   └── context/                  # React Context providers
│   │       ├── AppContext.tsx        # Global app state
│   │       └── SocketContext.tsx     # Socket.IO connection
│   ├── public/                       # Static assets
│   ├── .env.local                    # Environment variables (optional)
│   ├── package.json
│   ├── tsconfig.json
│   ├── tailwind.config.js
│   ├── next.config.ts
│   └── README.md                     # Frontend documentation
│
├── rabbitmq and aws guide.pdf        # Deployment guide
└── README.md                          # This file
```

## 🚀 Getting Started

### Prerequisites

- Node.js (v18 or higher)
- MongoDB
- Redis
- RabbitMQ
- Cloudinary account

### Environment Variables

Create `.env` files in each service directory:

**backend/user/.env:**
```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
REDIS_URL=redis://localhost:6379
JWT_SECRET=your_jwt_secret
Rabbitmq_Host=localhost
Rabbitmq_Username=guest
Rabbitmq_Password=guest
CHAT_SERVICE=http://localhost:5002
```

**backend/chat/.env:**
```env
PORT=5002
MONGO_URI=your_mongodb_connection_string
USER_SERVICE=http://localhost:5000
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
JWT_SECRET=your_jwt_secret
```

**backend/mail/.env:**
```env
PORT=5003
Rabbitmq_Host=localhost
Rabbitmq_Username=guest
Rabbitmq_Password=guest
USER=your_gmail_address
PASSWORD=your_gmail_app_password
```

### Installation & Running

1. **Install dependencies for all services:**

```bash
# User service
cd backend/user
npm install

# Chat service
cd ../chat
npm install

# Mail service
cd ../mail
npm install

# Frontend
cd ../../frontend
npm install
```

2. **Build TypeScript for backend services:**

```bash
# In each backend service directory
npm run build
```

3. **Start all services:**

```bash
# Terminal 1 - User Service
cd backend/user
npm run dev

# Terminal 2 - Chat Service
cd backend/chat
npm run dev

# Terminal 3 - Mail Service
cd backend/mail
npm run dev

# Terminal 4 - Frontend
cd frontend
npm run dev
```

4. **Access the application:**
   - Frontend: http://localhost:3000
   - User Service: http://localhost:5000
   - Chat Service: http://localhost:5002

## 🔄 How It Works

### Authentication Flow
1. User navigates to `/login` and enters email address
2. User Service generates 6-digit OTP and stores in Redis (5-minute TTL)
3. OTP request published to RabbitMQ queue
4. Mail Service consumes queue and sends OTP email via Nodemailer
5. User redirected to `/verify?email={email}` and enters OTP
6. System validates OTP against Redis cache
7. On success, JWT token generated and stored in HTTP-only cookie (15 days)
8. User redirected to `/chat` with authenticated session
9. Protected routes verify JWT token on each request

### Messaging Flow
1. User authenticates and Socket.IO connection established with userId
2. Frontend fetches all user chats via REST API (`GET /api/v1/chat/all`)
3. User selects chat and joins specific Socket.IO room (`joinChat` event)
4. User types message and sends via REST API (`POST /api/v1/message`)
5. Backend saves message to MongoDB and broadcasts via Socket.IO (`newMessage` event)
6. Real-time delivery to all online users in the chat room
7. When recipient opens chat, messages marked as seen (`messagesSeen` event)
8. Read receipts updated in real-time for sender
9. Unseen message count tracked and updated per conversation
10. Chat list automatically re-sorted by latest message timestamp

### Image Sharing Flow
1. User selects image file via file picker
2. Frontend validates file type and size
3. Image uploaded to Cloudinary via Multer middleware
4. Cloudinary returns secure URL and public ID
5. Message created with image metadata
6. Image displayed with thumbnail in chat
7. Full-size image accessible via Cloudinary CDN

### Real-Time Features Implementation
- **Online Status**: Socket.IO tracks connected users via `connection` and `disconnect` events, broadcasts list to all clients
- **Typing Indicators**: Debounced `typing` and `stopTyping` events (2-second timeout) emitted to chat room
- **Message Delivery**: Instant broadcast to chat room participants via Socket.IO rooms
- **Read Receipts**: Automatic marking when recipient views chat, updates `seen` field and `seenAt` timestamp
- **Presence Tracking**: Online users array maintained in SocketContext, updated on connection changes

## 📊 Database Schema

### User Collection
```typescript
{
  _id: ObjectId,
  name: string,
  email: string (unique),
  createdAt: Date,
  updatedAt: Date
}
```

### Chat Collection
```typescript
{
  _id: ObjectId,
  users: [string],  // Array of user IDs
  latestMessage: {
    text: string,
    sender: string
  },
  createdAt: Date,
  updatedAt: Date
}
```

### Messages Collection
```typescript
{
  _id: ObjectId,
  chatId: ObjectId,
  sender: string,
  text?: string,
  image?: {
    url: string,
    publicId: string
  },
  messageType: "text" | "image",
  seen: boolean,
  seenAt?: Date,
  createdAt: Date,
  updatedAt: Date
}
```

## 🎯 API Endpoints

### User Service (Port 5000)

#### Authentication
- `POST /api/v1/login` - Send OTP to email
  - Body: `{ email: string }`
  - Response: `{ success: true, message: "OTP sent to email" }`
  
- `POST /api/v1/verify` - Verify OTP and login
  - Body: `{ email: string, otp: string }`
  - Response: `{ success: true, message: "Login successful", token: string, user: User }`
  - Sets JWT cookie with 15-day expiration

#### User Management
- `GET /api/v1/me` - Get current user profile (Protected)
  - Headers: `Authorization: Bearer {token}` or Cookie
  - Response: `{ success: true, user: User }`

- `POST /api/v1/update/user` - Update user name (Protected)
  - Body: `{ name: string }`
  - Response: `{ success: true, message: "User updated", user: User }`

- `GET /api/v1/user/all` - Get all registered users (Protected)
  - Response: `{ success: true, users: User[] }`

- `GET /api/v1/user/:id` - Get specific user by ID (Protected)
  - Response: `{ success: true, user: User }`

### Chat Service (Port 5002)

#### Chat Management
- `POST /api/v1/chat/new` - Create new chat or get existing (Protected)
  - Body: `{ userId: string }` (other user's ID)
  - Response: `{ success: true, chat: Chat }`

- `GET /api/v1/chat/all` - Get all user chats with unseen counts (Protected)
  - Response: `{ success: true, chats: Chat[] }`

#### Messaging
- `POST /api/v1/message` - Send text or image message (Protected)
  - Body (text): `{ chatId: string, text: string }`
  - Body (image): `FormData { chatId: string, image: File }`
  - Response: `{ success: true, message: Message }`
  - Broadcasts `newMessage` event via Socket.IO

- `GET /api/v1/message/:chatId` - Get all messages in chat (Protected)
  - Response: `{ success: true, messages: Message[] }`
  - Automatically marks messages as seen

## 🔌 WebSocket Events (Socket.IO)

### Client → Server Events

- `typing` - User started typing in a chat
  - Payload: `{ chatId: string, userId: string }`
  - Broadcasts to other users in chat room

- `stopTyping` - User stopped typing
  - Payload: `{ chatId: string, userId: string }`
  - Broadcasts to other users in chat room

- `joinChat` - Join specific chat room
  - Payload: `{ chatId: string }`
  - Adds socket to room for targeted broadcasts

- `leaveChat` - Leave chat room
  - Payload: `{ chatId: string }`
  - Removes socket from room

### Server → Client Events

- `getOnlineUser` - List of currently online users
  - Payload: `{ onlineUsers: string[] }` (array of user IDs)
  - Emitted on connection/disconnection changes

- `newMessage` - New message received in chat
  - Payload: `{ message: Message }`
  - Emitted to all users in chat room

- `messagesSeen` - Messages marked as seen by recipient
  - Payload: `{ chatId: string, userId: string, seenAt: Date }`
  - Emitted to sender when recipient views chat

- `userTyping` - Another user is typing
  - Payload: `{ chatId: string, userId: string }`
  - Emitted to other users in chat room

- `userStoppedTyping` - User stopped typing
  - Payload: `{ chatId: string, userId: string }`
  - Emitted to other users in chat room

### Connection Events

- `connection` - New socket connection established
  - Server tracks userId from query params
  - Adds user to online users list
  - Broadcasts updated online users

- `disconnect` - Socket connection closed
  - Removes user from online users list
  - Broadcasts updated online users

## 🎨 UI/UX Features

### Design System
- **Color Scheme**: Dark theme (gray-900, gray-800, gray-700) with blue-600 accents
- **Typography**: System fonts with clear hierarchy and readable sizes
- **Spacing**: Consistent padding and margins following 4px grid
- **Borders**: Subtle gray borders for visual separation
- **Glassmorphism**: Modern frosted glass effects on key components

### Responsive Design
- **Mobile-First**: Optimized for mobile devices, scales up to desktop
- **Breakpoints**: Tailwind CSS responsive utilities for all screen sizes
- **Collapsible Sidebar**: Hamburger menu on mobile, persistent on desktop
- **Touch-Friendly**: Large tap targets (44px minimum) for mobile
- **Flexible Layouts**: Flexbox and Grid for adaptive layouts

### Interactive Elements
- **Real-Time Updates**: Messages appear instantly without page refresh
- **Image Preview**: Preview images before sending
- **Smooth Animations**: CSS transitions for hover, focus, and state changes
- **Loading States**: Spinners and disabled states during async operations
- **Toast Notifications**: Non-intrusive notifications for user actions
- **Unseen Message Badges**: Blue badges showing unread count per chat
- **Online Indicators**: Green dot for online, gray for offline users
- **Typing Indicators**: "User is typing..." text in chat header
- **Read Receipts**: Single check (sent), double check (seen) on messages

### Accessibility
- **Semantic HTML**: Proper heading hierarchy and landmark elements
- **Keyboard Navigation**: Full keyboard support for all interactions
- **ARIA Labels**: Screen reader friendly labels and descriptions
- **Focus Management**: Visible focus indicators and logical tab order
- **Color Contrast**: WCAG AA compliant contrast ratios
- **Alt Text**: Descriptive alt text for images

### Performance Optimizations
- **Code Splitting**: Next.js automatic code splitting per route
- **Lazy Loading**: Components loaded on demand
- **Image Optimization**: Next.js Image component with automatic optimization
- **Memoization**: React.memo and useMemo to prevent unnecessary re-renders
- **Debouncing**: Typing indicators debounced to reduce event spam
- **Efficient Re-renders**: Context split into AppContext and SocketContext

## 🔐 Security Features

### Authentication & Authorization
- **JWT Tokens**: Stateless authentication with HS256 algorithm
- **HTTP-only Cookies**: Prevents XSS attacks by making tokens inaccessible to JavaScript
- **Token Expiration**: 15-day expiration with automatic cleanup
- **Protected Routes**: Middleware validates JWT on every protected endpoint
- **User Context**: Frontend checks authentication state before rendering protected pages

### Rate Limiting & Abuse Prevention
- **Redis-based Rate Limiting**: Prevents OTP spam (e.g., 3 requests per 15 minutes)
- **OTP Expiration**: 5-minute TTL on OTPs stored in Redis
- **Request Throttling**: Limits on API endpoints to prevent abuse

### Data Protection
- **Input Validation**: Server-side validation on all user inputs
- **Sanitization**: Prevents NoSQL injection and XSS attacks
- **File Upload Validation**: Checks file type, size, and format before upload
- **Cloudinary Security**: Secure image storage with access control
- **Environment Variables**: Sensitive credentials stored in .env files (not committed)

### Network Security
- **CORS Configuration**: Restricts cross-origin requests to trusted domains
- **HTTPS Ready**: Production deployment should use HTTPS/TLS
- **Secure Headers**: Security headers for XSS, clickjacking protection
- **Socket.IO Authentication**: Validates user before establishing WebSocket connection

### Database Security
- **MongoDB Connection**: Secure connection strings with authentication
- **Schema Validation**: Mongoose schemas enforce data integrity
- **Indexed Queries**: Prevents performance-based DoS attacks
- **No Sensitive Data Exposure**: Passwords not stored (passwordless auth)

## 📈 Scalability & Performance

### Microservices Architecture
- **Independent Scaling**: Each service (User, Chat, Mail) can scale independently
- **Service Isolation**: Failures in one service don't affect others
- **Technology Flexibility**: Each service can use different tech stacks if needed
- **Load Balancing**: Services can be load-balanced separately

### Caching & Storage
- **Redis Caching**: Fast in-memory storage for OTPs and rate limiting
- **MongoDB Indexing**: Optimized queries with indexes on frequently queried fields
- **Cloudinary CDN**: Global CDN for fast image delivery worldwide
- **Connection Pooling**: Reuses database connections for better performance

### Asynchronous Processing
- **RabbitMQ Message Queue**: Decouples email sending from request/response cycle
- **Non-blocking I/O**: Node.js event loop handles concurrent requests efficiently
- **Background Jobs**: Email processing happens asynchronously

### Real-Time Optimization
- **Socket.IO Rooms**: Efficient message broadcasting to specific chat participants
- **Event Debouncing**: Typing indicators debounced to reduce network traffic
- **Selective Broadcasting**: Events only sent to relevant users, not all connections
- **Connection Pooling**: Reuses WebSocket connections

### Frontend Performance
- **Next.js App Router**: Server-side rendering and streaming for faster initial load
- **Code Splitting**: Automatic route-based code splitting
- **React 19**: Latest React features for optimal rendering
- **Lazy Loading**: Components and images loaded on demand
- **Memoization**: Prevents unnecessary re-renders with React.memo and useMemo

### Database Optimization
- **Indexed Fields**: Indexes on userId, chatId, email for fast lookups
- **Lean Queries**: Only fetch required fields to reduce payload size
- **Pagination Ready**: Structure supports pagination for large datasets
- **Aggregation Pipeline**: Efficient queries for complex data operations

### Deployment Considerations
- **Horizontal Scaling**: Add more instances of services behind load balancer
- **Container Ready**: Services can be containerized with Docker
- **Cloud Deployment**: Ready for AWS, Azure, or GCP deployment
- **Monitoring**: Structured for logging and monitoring integration

## 🛠️ Development

### Available Scripts

**Backend Services (User, Chat, Mail):**
```bash
npm run dev      # Development mode with hot reload (ts-node-dev)
npm run build    # Compile TypeScript to JavaScript (dist/)
npm start        # Run production build from dist/
```

**Frontend:**
```bash
npm run dev      # Next.js development server (http://localhost:3000)
npm run build    # Production build with optimizations
npm start        # Start production server
npm run lint     # Run ESLint for code quality
```

### Development Workflow

1. **Start Infrastructure Services:**
   ```bash
   # Start MongoDB (default port 27017)
   mongod
   
   # Start Redis (default port 6379)
   redis-server
   
   # Start RabbitMQ (default port 5672, management UI: 15672)
   rabbitmq-server
   ```

2. **Start Backend Services:**
   ```bash
   # Terminal 1 - User Service
   cd backend/user
   npm run dev
   
   # Terminal 2 - Chat Service
   cd backend/chat
   npm run dev
   
   # Terminal 3 - Mail Service
   cd backend/mail
   npm run dev
   ```

3. **Start Frontend:**
   ```bash
   # Terminal 4 - Frontend
   cd frontend
   npm run dev
   ```

4. **Access Application:**
   - Frontend: http://localhost:3000
   - User Service: http://localhost:5000
   - Chat Service: http://localhost:5002
   - Mail Service: http://localhost:5003 (internal only)
   - RabbitMQ Management: http://localhost:15672 (guest/guest)

### Code Quality

- **TypeScript**: Strict type checking enabled in all services
- **ESLint**: Configured for Next.js and TypeScript best practices
- **Consistent Formatting**: Follow project conventions
- **Error Handling**: TryCatch wrapper for consistent error responses
- **Git Hooks**: Consider adding pre-commit hooks for linting

### Debugging

- **Backend**: Use VS Code debugger or `console.log` statements
- **Frontend**: React DevTools and browser console
- **Socket.IO**: Monitor events in browser Network tab (WS)
- **RabbitMQ**: Use management UI to monitor queues
- **Redis**: Use `redis-cli` to inspect cached data
- **MongoDB**: Use MongoDB Compass or `mongosh` for database inspection

## 🐛 Troubleshooting

### Common Issues

**MongoDB Connection Failed:**
- Ensure MongoDB is running: `mongod` or check service status
- Verify `MONGO_URI` in `.env` files is correct
- Check network connectivity and firewall settings

**Redis Connection Error:**
- Start Redis server: `redis-server`
- Verify Redis is running: `redis-cli ping` (should return PONG)
- Check `REDIS_URL` in user service `.env`

**RabbitMQ Connection Failed:**
- Start RabbitMQ: `rabbitmq-server`
- Check management UI: http://localhost:15672
- Verify credentials in `.env` files (default: guest/guest)

**OTP Email Not Received:**
- Check Mail Service logs for errors
- Verify Gmail credentials in `backend/mail/.env`
- Enable "Less secure app access" or use App Password for Gmail
- Check RabbitMQ queue for pending messages

**Socket.IO Connection Issues:**
- Verify Chat Service is running on port 5002
- Check browser console for WebSocket errors
- Ensure CORS is properly configured
- Verify JWT token is valid

**Images Not Uploading:**
- Check Cloudinary credentials in `backend/chat/.env`
- Verify file size is within limits
- Check network connectivity to Cloudinary
- Review multer middleware configuration

**JWT Token Expired:**
- Token expires after 15 days
- User needs to login again
- Check `JWT_SECRET` matches across services

### Error Messages

**"User not found":**
- User hasn't registered yet
- Email might be incorrect
- Check MongoDB User collection

**"Invalid OTP":**
- OTP expired (5-minute limit)
- Wrong OTP entered
- Request new OTP

**"Rate limit exceeded":**
- Too many OTP requests
- Wait 15 minutes before retrying
- Check Redis for rate limit keys

## 🚀 Deployment

### Production Checklist

- [ ] Set strong `JWT_SECRET` values
- [ ] Use production MongoDB cluster (MongoDB Atlas)
- [ ] Configure Redis with persistence
- [ ] Set up RabbitMQ cluster for reliability
- [ ] Use environment-specific `.env` files
- [ ] Enable HTTPS/TLS for all services
- [ ] Configure CORS for production domains
- [ ] Set up logging and monitoring (e.g., Winston, PM2)
- [ ] Implement rate limiting on all endpoints
- [ ] Use process manager (PM2, Docker, Kubernetes)
- [ ] Set up CDN for frontend assets
- [ ] Configure database backups
- [ ] Implement health check endpoints
- [ ] Set up error tracking (Sentry, Rollbar)

### Deployment Options

**Option 1: Traditional VPS (DigitalOcean, Linode)**
- Deploy each service on separate ports
- Use Nginx as reverse proxy
- PM2 for process management
- Let's Encrypt for SSL certificates

**Option 2: Containerized (Docker + Docker Compose)**
- Create Dockerfile for each service
- Use docker-compose.yml for orchestration
- Deploy to any container platform

**Option 3: Cloud Platform (AWS, Azure, GCP)**
- User Service → AWS Lambda or EC2
- Chat Service → EC2 with Socket.IO support
- Mail Service → Lambda or EC2
- MongoDB → MongoDB Atlas
- Redis → AWS ElastiCache or Redis Cloud
- RabbitMQ → Amazon MQ or CloudAMQP
- Frontend → Vercel, Netlify, or AWS Amplify

**Option 4: Kubernetes**
- Create Kubernetes manifests for each service
- Use Helm charts for deployment
- Auto-scaling based on load
- Service mesh for inter-service communication

### Environment Variables for Production

Update all `.env` files with production values:
- Use strong, unique `JWT_SECRET`
- Production database URLs
- Production Cloudinary account
- Production email credentials
- Production domain URLs for CORS

## 📚 Future Enhancements

### Planned Features
- **Group Chats**: Multi-user conversations with admin controls
- **Voice Messages**: Record and send audio messages
- **Video Calls**: WebRTC-based video calling
- **File Sharing**: Upload and share documents, PDFs, etc.
- **Message Reactions**: Emoji reactions to messages
- **Message Editing**: Edit sent messages within time limit
- **Message Deletion**: Delete messages for self or everyone
- **Message Search**: Full-text search across all messages
- **User Blocking**: Block unwanted users
- **Push Notifications**: Browser and mobile push notifications
- **Dark/Light Theme Toggle**: User preference for theme
- **Message Forwarding**: Forward messages to other chats
- **Chat Archiving**: Archive old conversations
- **User Status**: Custom status messages
- **Last Seen**: Show when user was last online
- **Media Gallery**: View all shared images in a chat
- **Chat Export**: Export chat history as PDF/JSON

### Technical Improvements
- **End-to-End Encryption**: Encrypt messages for privacy
- **Message Pagination**: Load messages in chunks for performance
- **Infinite Scroll**: Lazy load older messages
- **Service Workers**: Offline support and caching
- **GraphQL API**: Alternative to REST for flexible queries
- **Redis Pub/Sub**: Scale Socket.IO across multiple servers
- **Database Sharding**: Horizontal scaling for MongoDB
- **CDN Integration**: Serve static assets via CDN
- **Automated Testing**: Unit, integration, and e2e tests
- **CI/CD Pipeline**: Automated deployment on git push
- **Docker Compose**: Simplified local development setup
- **API Documentation**: Swagger/OpenAPI documentation
- **Monitoring Dashboard**: Real-time metrics and alerts
- **Load Testing**: Performance testing with k6 or Artillery

### UI/UX Enhancements
- **Emoji Picker**: Native emoji selector
- **GIF Support**: Integrate GIPHY or Tenor
- **Stickers**: Custom sticker packs
- **Message Threads**: Reply to specific messages
- **Mentions**: @mention users in group chats
- **Rich Text Editor**: Bold, italic, code formatting
- **Link Previews**: Show preview cards for URLs
- **Drag & Drop**: Drag files to upload
- **Keyboard Shortcuts**: Power user shortcuts
- **Customizable Themes**: User-defined color schemes
- **Chat Backgrounds**: Custom chat wallpapers
- **Sound Notifications**: Audio alerts for new messages

## 🤝 Contributing

Contributions are welcome! This project demonstrates modern full-stack development practices with microservices architecture.

### How to Contribute
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Contribution Guidelines
- Follow existing code style and conventions
- Write meaningful commit messages
- Add comments for complex logic
- Update documentation for new features
- Test your changes thoroughly
- Ensure TypeScript types are correct

## 📝 License

ISC

## 👥 Authors

Built with ❤️ for demonstration purposes

## 🙏 Acknowledgments

- Next.js team for the amazing framework
- Socket.IO for real-time communication
- MongoDB for flexible database
- Cloudinary for image hosting
- RabbitMQ for message queuing
- Redis for caching and rate limiting

## 📞 Support

For questions or issues, please open an issue on the repository.

---

**Note**: This application demonstrates production-ready patterns including microservices architecture, real-time communication with Socket.IO, asynchronous message queuing with RabbitMQ, and modern frontend development with Next.js 15 and React 19. Perfect for learning full-stack development with TypeScript!
