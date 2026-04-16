# Day 1 - Frontend Setup

Welcome to Day 1 of the course **Build a Custom AI Chatbot That Learns from Websites**.

Today our goal is to build the frontend foundation of the application and prepare the project structure for future development.

---

# 🎯 What We Will Complete Today

By the end of Day 1, you will have:

- Root project structure created
- Frontend application initialized
- Dockerized frontend environment
- Docker Compose configuration ready
- Homepage created
- App running on localhost:3000

---

# 📁 Project Structure

```bash
project-root/
│── client/
│   │── src/
│   │   │── pages/
│   │   │   │── index.js
│   │── package.json
│   │── Dockerfile
│── docker-compose.yml
│── instructions/
│   │── day1/
│   │   │── readme.md
```

---

# 🛠 Step 1 - Create Root Folder

Create the main project folder:

```bash
mkdir custom-chatbot
cd custom-chatbot
```

---

# 🛠 Step 2 - Create Client Folder

```bash
mkdir client
```

This folder contains the frontend application built with Next.js.

---

# 🛠 Step 3 - Create package.json

Inside `client/package.json`

```json
{
  "name": "custom_chatbot",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start"
  },
  "dependencies": {
    "next": "^15.5.15",
    "react": "18.3.1",
    "react-dom": "18.3.1"
  },
  "devDependencies": {
    "classnames": "2.5.1",
    "eslint": "9.33.0",
    "eslint-config-next": "15.1.6"
  }
}
```

---

# 🛠 Step 4 - Create Dockerfile

Inside `client/Dockerfile`

```Dockerfile
FROM node:18.20.4-alpine3.20

WORKDIR /usr/src/app

COPY ./package.json .
RUN npm install

COPY . .

EXPOSE 3000

RUN addgroup app && adduser -SG app app
RUN chown -R app:app .
USER app
```

---

# 🛠 Step 5 - Create Homepage

Inside `client/src/pages/index.js`

```javascript
const index = () => (
  <div>
    <h1>Welcome to the Custom Chatbot Application</h1>
    <p>This is the home page. Use the navigation to explore the features.</p>
  </div>
);

export default index;
```

---

# 🛠 Step 6 - Create docker-compose.yml

Inside root folder:

```yml
services:
  client:
    restart: always
    build:
      dockerfile: Dockerfile
      context: ./client
    environment:
      - CHOKIDAR_USEPOLLING=true
      - WATCHPACK_POLLING=true
    ports:
      - "3000:3000"
    volumes:
      - ./client:/usr/src/app
      - /usr/src/app/node_modules
    command: npm run dev
```

---

# ▶️ Step 7 - Run Application

```bash
docker-compose -f docker-compose.yml up --build -d
```

---

# ✅ Final Result

Open browser:

```bash
http://localhost:3000
```

You should see the homepage running successfully.

---

# 📚 What You Learned Today

- How to structure a scalable project
- How to dockerize a Next.js frontend
- How Docker Compose manages services
- How live development works inside containers

---

# ⏭ Next Day

Day 2 we will begin backend development using Django.

We will create APIs and prepare the server architecture.

---

# 🚀 Great Start

Day 1 is complete.
