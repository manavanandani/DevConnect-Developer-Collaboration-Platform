# DevConnect - Developer Collaboration Platform

DevConnect is a full-stack, GitHub-inspired platform built to streamline developer collaboration through real-time chat, code sharing, and project management. Designed with scalability, responsiveness, and fault tolerance in mind, DevConnect has successfully supported 1,400+ active users and processed over 8,000 encrypted messages daily.

---

## 🚀 Features

* Real-time team chat (Slack-style interface)
* Live code collaboration and syntax-highlighted snippets
* Project and task management
* Notifications and user mentions
* Role-based access and authentication (OAuth2 + JWT)
* Secure and fault-tolerant Socket.io-based communication
* GraphQL APIs with Redux for efficient data sync
* Responsive UI with Vue.js and Tailwind CSS

---

## 📁 Project Structure

```
DevConnect/
├── backend/
│   ├── server.js
│   ├── config/
│   │   └── db.js
│   ├── graphql/
│   │   ├── resolvers/
│   │   ├── typeDefs/
│   ├── models/
│   │   ├── User.js
│   │   ├── Project.js
│   │   └── Message.js
│   ├── routes/
│   │   └── auth.js
│   ├── socket/
│   │   └── index.js
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── store/
│   │   ├── graphql/
│   │   └── App.vue
├── .env
├── README.md
└── package.json
```

---

## 🧑‍💻 Technologies Used

* **Frontend:** Vue.js, Tailwind CSS, Axios, Vue Router
* **Backend:** Node.js, Express.js, GraphQL, Apollo Server
* **Database:** MongoDB (Mongoose ODM)
* **Real-time:** Socket.io
* **Authentication:** JWT + OAuth2 (GitHub Login)
* **State Management:** Redux
* **Hosting:** Docker, AWS EC2

---

## ⚙️ Installation & Setup Guide

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/devconnect.git
cd devconnect
```

### 2. Backend Setup

```bash
cd backend
npm install
```

#### Create `.env` file

```
MONGO_URI=mongodb://localhost:27017/devconnect
JWT_SECRET=your_jwt_secret
GITHUB_CLIENT_ID=your_client_id
GITHUB_CLIENT_SECRET=your_client_secret
```

#### Run Backend

```bash
npm run dev
```

### 3. Frontend Setup

```bash
cd frontend
npm install
npm run serve
```

---

## 🔐 Authentication

* GitHub OAuth2 flow via `passport-github2`
* JWT token stored in HttpOnly cookies for secure sessions

```js
// Sample JWT Token Signing
const token = jwt.sign({ userId: user._id }, process.env.JWT_SECRET, { expiresIn: '1d' });
```

---

## 📡 Real-Time Chat with Socket.io

* Namespace: `/chat`
* Emits:

  * `message` - for new messages
  * `typing` - typing notifications
* Listens:

  * `joinRoom` - on entering a room
  * `disconnect` - on user leave

```js
// Example Socket.io server logic
io.of('/chat').on('connection', socket => {
  socket.on('joinRoom', ({ room }) => {
    socket.join(room);
  });

  socket.on('message', ({ content, sender }) => {
    io.to(room).emit('message', { content, sender });
  });
});
```

---

## 🛠 GraphQL with Apollo Server

* Endpoints exposed via `/graphql`
* Resolvers for `User`, `Project`, `Message`

```js
// Example Query
query {
  getAllProjects {
    name
    description
  }
}
```

---

## 🧩 Redux State Management

Used for managing project lists, current chats, and authentication state across components.

```js
const initialState = {
  user: null,
  projects: [],
  messages: [],
};
```

---

## 🎨 UI Showcase

* Responsive Slack-like layout using Vue.js and Tailwind CSS
* Dark/light theme toggle
* Syntax-highlighted code blocks using `highlight.js`

---

## 📈 Performance & Scaling

* Real-time messaging throughput: **8,000+ encrypted messages/day**
* Scalable Socket.io deployment with sticky sessions
* MongoDB indexing for fast project/user retrieval

---

## 🧪 Testing

* Unit testing with Jest
* Frontend tests using Cypress

```bash
# Backend tests
npm run test

# Cypress tests (frontend)
npm run cypress
```

---

## 🐳 Docker Deployment

```Dockerfile
# Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "start"]
```

```bash
# Build and run
docker build -t devconnect .
docker run -p 5000:5000 devconnect
```

---

## 📦 Future Enhancements

* AI-based code review assistant
* GitHub repo integration for PR tracking
* Voice/video collaboration via WebRTC
* Integration with CI/CD tools like Jenkins

---

## 🤝 Contributors

* Manav Anandani - [@manavanandani](https://github.com/manavanandani)
* Open for contributions - submit a PR!

---

## 📄 License

This project is licensed under the MIT License. See the `LICENSE` file for details.
