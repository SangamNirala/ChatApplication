# Chat Application - Frontend

Modern, responsive Next.js frontend for the real-time chat application with Socket.IO integration.

## 🎨 Overview

This is the client-side application built with Next.js 15 and React 19, providing a seamless real-time chat experience with modern UI/UX patterns.

## 🛠️ Technology Stack

- **Framework**: Next.js 15.3.4 (App Router)
- **React**: 19.0.0
- **TypeScript**: Type-safe development
- **Styling**: Tailwind CSS 4
- **Real-time**: Socket.IO Client 4.8.1
- **HTTP Client**: Axios 1.10.0
- **State Management**: React Context API
- **Notifications**: React Hot Toast
- **Icons**: Lucide React
- **Cookie Management**: js-cookie
- **Date Formatting**: Moment.js

## 📁 Project Structure

```
frontend/
├── src/
│   ├── app/                    # Next.js App Router pages
│   │   ├── chat/              # Main chat interface
│   │   ├── login/             # Login page
│   │   ├── profile/           # User profile page
│   │   ├── verify/            # OTP verification page
│   │   ├── layout.tsx         # Root layout
│   │   └── page.tsx           # Home (redirects to chat)
│   ├── components/            # Reusable components
│   │   ├── ChatHeader.tsx     # Chat header with user info
│   │   ├── ChatMessages.tsx   # Message list display
│   │   ├── ChatSidebar.tsx    # Sidebar with chat list
│   │   ├── Loading.tsx        # Loading spinner
│   │   ├── MessageInput.tsx   # Message input with image upload
│   │   └── VerifyOtp.tsx      # OTP verification form
│   └── context/               # React Context providers
│       ├── AppContext.tsx     # Global app state
│       └── SocketContext.tsx  # Socket.IO connection
├── public/                    # Static assets
├── package.json
├── tsconfig.json
├── tailwind.config.js
└── next.config.ts
```

## ✨ Features

### Pages

#### Login Page (`/login`)
- Email-based authentication
- OTP request functionality
- Clean, modern UI with loading states
- Automatic redirect if already authenticated

#### Verify Page (`/verify`)
- 6-digit OTP input
- Email verification
- Resend OTP functionality
- Auto-redirect on successful verification

#### Chat Page (`/chat`)
- Real-time message display
- Chat list with unseen message counts
- User search and new chat creation
- Online/offline status indicators
- Typing indicators
- Message read receipts
- Image sharing capability
- Responsive sidebar

#### Profile Page (`/profile`)
- View and edit display name
- User information display
- Back navigation to chat

### Components

#### ChatSidebar
- Displays all active conversations
- Shows unseen message count per chat
- User search functionality
- Online/offline status
- Create new chat
- Profile and logout buttons
- Mobile-responsive with hamburger menu

#### ChatMessages
- Scrollable message list
- Differentiated sent/received messages
- Image message support
- Timestamp display
- Read receipt indicators (single/double check)
- Auto-scroll to latest message
- Message deduplication

#### MessageInput
- Text message input
- Image upload with preview
- Send button with loading state
- Typing indicator trigger
- File validation

#### ChatHeader
- Display selected user info
- Online status indicator
- Typing indicator
- Mobile menu toggle

### Context Providers

#### AppContext
- User authentication state
- User profile management
- Chat list management
- User list management
- Logout functionality
- API service URLs

#### SocketContext
- Socket.IO connection management
- Online users tracking
- Automatic connection on user login
- Cleanup on disconnect

## 🔌 Real-Time Features

### Socket.IO Events

**Emitted Events:**
- `typing` - When user starts typing
- `stopTyping` - When user stops typing
- `joinChat` - Join specific chat room
- `leaveChat` - Leave chat room

**Listened Events:**
- `getOnlineUser` - Receive list of online users
- `newMessage` - Receive new message
- `messagesSeen` - Messages marked as read
- `userTyping` - Other user typing
- `userStoppedTyping` - Other user stopped typing

## 🎯 State Management

### Global State (AppContext)
```typescript
{
  user: User | null,
  isAuth: boolean,
  loading: boolean,
  chats: Chats[] | null,
  users: User[] | null,
  setUser: Function,
  setIsAuth: Function,
  logoutUser: Function,
  fetchChats: Function,
  fetchUsers: Function,
  setChats: Function
}
```

### Socket State (SocketContext)
```typescript
{
  socket: Socket | null,
  onlineUsers: string[]
}
```

## 🔐 Authentication Flow

1. User enters email on `/login`
2. OTP sent to email
3. Redirect to `/verify?email={email}`
4. User enters OTP
5. JWT token stored in cookie (15 days)
6. Redirect to `/chat`
7. Protected routes check authentication

## 📡 API Integration

### Service URLs
- User Service: `http://localhost:5000`
- Chat Service: `http://localhost:5002`

### API Calls

**User Service:**
- `POST /api/v1/login` - Request OTP
- `POST /api/v1/verify` - Verify OTP
- `GET /api/v1/me` - Get current user
- `POST /api/v1/update/user` - Update profile
- `GET /api/v1/user/all` - Get all users

**Chat Service:**
- `POST /api/v1/chat/new` - Create chat
- `GET /api/v1/chat/all` - Get user chats
- `POST /api/v1/message` - Send message
- `GET /api/v1/message/:chatId` - Get messages

## 🎨 UI/UX Features

### Design System
- **Color Scheme**: Dark theme (gray-900, gray-800, gray-700)
- **Accent Color**: Blue-600 for primary actions
- **Typography**: System fonts with clear hierarchy
- **Spacing**: Consistent padding and margins
- **Borders**: Subtle gray borders for separation

### Responsive Design
- Mobile-first approach
- Collapsible sidebar on mobile
- Touch-friendly buttons
- Optimized for all screen sizes

### User Feedback
- Toast notifications for actions
- Loading states for async operations
- Disabled states for invalid actions
- Visual feedback for interactions

### Animations
- Smooth transitions
- Scroll animations
- Hover effects
- Loading spinners

## 🚀 Getting Started

### Prerequisites
- Node.js 18+
- Backend services running

### Installation

```bash
npm install
```

### Environment Setup

The frontend connects to backend services at:
- User Service: `http://localhost:5000`
- Chat Service: `http://localhost:5002`

These are configured in `src/context/AppContext.tsx`.

### Development

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

### Build

```bash
npm run build
npm start
```

## 📦 Key Dependencies

```json
{
  "next": "15.3.4",
  "react": "^19.0.0",
  "socket.io-client": "^4.8.1",
  "axios": "^1.10.0",
  "react-hot-toast": "^2.5.2",
  "lucide-react": "^0.525.0",
  "js-cookie": "^3.0.5",
  "moment": "^2.30.1",
  "tailwindcss": "^4"
}
```

## 🔧 Configuration Files

### next.config.ts
Next.js configuration for app behavior

### tsconfig.json
TypeScript compiler options

### tailwind.config.js
Tailwind CSS customization

### eslint.config.mjs
ESLint rules for code quality

## 🎯 Key Features Implementation

### Real-Time Message Updates
- Socket.IO connection established on login
- Messages instantly appear without refresh
- Optimistic UI updates

### Typing Indicators
- Debounced typing events (2-second timeout)
- Visual indicator in chat header
- Automatic cleanup

### Read Receipts
- Single check: Message sent
- Double check: Message seen
- Timestamp of when seen

### Unseen Message Counter
- Badge on chat list items
- Resets when chat opened
- Updates in real-time

### Chat Sorting
- Automatically sorts by latest message
- Moves active chat to top
- Persists across sessions

### Image Sharing
- File picker integration
- Image preview before send
- Cloudinary upload
- Thumbnail in message list

## 🐛 Error Handling

- Network error notifications
- Failed message retry
- Authentication error redirects
- Graceful degradation

## ♿ Accessibility

- Semantic HTML
- Keyboard navigation
- ARIA labels
- Focus management
- Screen reader friendly

## 📱 Mobile Optimization

- Touch-friendly interface
- Responsive layout
- Mobile menu
- Optimized images
- Fast loading

## 🔒 Security

- JWT token in HTTP-only cookies
- XSS protection
- CSRF considerations
- Input sanitization
- Secure file uploads

## 🚀 Performance

- Code splitting
- Lazy loading
- Image optimization
- Memoization
- Efficient re-renders

## 📈 Future Enhancements

- Voice messages
- Video calls
- Group chats
- Message reactions
- File sharing
- Message search
- Dark/light theme toggle
- Push notifications

## 🤝 Contributing

Follow Next.js and React best practices when contributing.

---

Built with Next.js 15, React 19, and Socket.IO for real-time communication.
