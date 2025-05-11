# 🚀 Step-by-Step Guide to Setting Up and Running the Skill-Sharing Website 🌱

## ⿡ Basics: What You Need to Know 🤨
Before we dive in, let’s understand what this project is about.

- *What is it?* 🤔  
  This is a *skill-sharing website* where users can *register, log in, and search for people with skills*.
- *Tech Stack* 🛠  
  - *Frontend:* HTML, CSS, JavaScript
  - *Backend:* Node.js, Express.js
  - *Database:* MongoDB (Atlas)
  - *Authentication:* JSON Web Tokens (JWT)

---

## ⿢ Installations: What to Download 

### 🔹 Install Node.js (Backend Runtime)
💻 *Download and install Node.js* from [https://nodejs.org](https://nodejs.org) (LTS version recommended).  
📌 *To check if it's installed, run:*
sh
node -v
npm -v

---

### 🔹 Install VS Code (Code Editor)
💻 *Download and install VS Code* from [https://code.visualstudio.com/](https://code.visualstudio.com/).

---

### 🔹 Install MongoDB (Database)
We are using *MongoDB Atlas (cloud database)*. To set it up:
1. Go to [https://www.mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas) 🌍
2. *Sign up* (or log in if you already have an account).
3. Click *Create Cluster* → Choose *Shared Cluster* (free tier).
4. Select a cloud provider & region 🌎.
5. *Whitelist your IP:* Go to Network Access → Add IP *0.0.0.0/0* (Allows access from anywhere).
6. *Create a database user:* Add a username & password (REMEMBER THIS! You’ll need it soon!) 🔑.
7. Click *Connect* → Choose *Connect Your Application*.
8. Copy the connection string (it looks like this):
   sh
   mongodb+srv://<your-username>:<your-password>@cluster.mongodb.net/<dbname>?retryWrites=true&w=majority
   
9. *Replace* <your-username>, <your-password>, and <dbname> with your credentials.

📌 *DO NOT use my credentials from Postman. You need to create your own!*

---

## ⿣ Setting Up the Project 📚
### 🔹 1. Create a Project Folder
📌 Open *VS Code, then open the terminal (Ctrl + `* on Windows, *Cmd + `* on Mac).
sh
mkdir skill-sharing-website
cd skill-sharing-website

---

### 🔹 2. Initialize a Node.js Project 📦
📌 Inside your *project folder*, run:
sh
npm init -y

This will create a package.json file.
---

### 🔹 3. Install Dependencies 
sh
npm install express mongoose dotenv cors jsonwebtoken bcryptjs multer

💚 *What are these for?*
- express → Web server framework
- mongoose → Connects Node.js to MongoDB
- dotenv → Manages environment variables
- cors → Handles Cross-Origin Resource Sharing
- jsonwebtoken → Used for authentication
- bcryptjs → Hashes passwords for security
- multer → Handles file uploads (e.g., profile pictures)
---

## ⿤ Setting Up the Backend 🌐

### 🔹 Create server.js
js
require('dotenv').config({ path: './.env' });
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
const authRoutes = require('./routes/auth');

const app = express();
app.use(express.json());
app.use(cors());
app.use('/uploads', express.static('uploads'));
app.use('/auth', authRoutes);

app.get("/", (req, res) => {
    res.send("✅ Server is running!");
});

mongoose.connect(process.env.MONGO_URI)
    .then(() => console.log('🔥 MongoDB Connected'))
    .catch(err => console.error('❌ MongoDB Connection Error:', err));

const PORT = process.env.PORT || 5000;
app.listen(PORT, () => console.log(`🚀 Server running on port ${PORT}`));


### 🔹 Create .env
env
MONGO_URI=mongodb+srv://<your-username>:<your-password>@cluster.mongodb.net/<dbname>
PORT=5000
JWT_SECRET=your_secret_key


### 🔹 Create routes/auth.js
js
const express = require('express');
const bcrypt = require('bcryptjs');
const jwt = require('jsonwebtoken');
const router = express.Router();

router.post('/register', async (req, res) => {
    // Registration logic here
});

router.post('/login', async (req, res) => {
    // Login logic here
});

module.exports = router;


## ⿥ Setting Up the Frontend 🎨

### 🔹 Create index.html
html
<!DOCTYPE html>
<html>
<head>
    <title>Skill Sharing</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Welcome to Skill Sharing</h1>
    <a href="register.html">Register</a>
    <a href="login.html">Login</a>
</body>
</html>


### 🔹 Create login.html
html
<!DOCTYPE html>
<html>
<head>
    <title>Login</title>
</head>
<body>
    <h2>Login</h2>
    <input type="text" id="username" placeholder="Username">
    <input type="password" id="password" placeholder="Password">
    <button onclick="login()">Login</button>
</body>
</html>


### 🔹 Create script.js
js
function login() {
    console.log("Logging in...");
}


### 🔹 Create styles.css
css
body {
    font-family: Arial, sans-serif;
}


## ⿦ Running the Project 🏃‍♂

### 🔹 Start the Server
sh
node server.js


✅ If everything is working, you should see:

🔥 MongoDB Connected
🚀 Server running on port 5000


🎉 *Congratulations! Your skill-sharing website is now up and running!* 
