# 🚀 Express + TypeScript Starter Boilerplate

A clean and beginner-friendly setup for running an **Express.js server with TypeScript**, **TSX auto-reload**, and essential backend utilities like **dotenv** and **bcrypt**.

---

## 📌 Features
- Express.js with TypeScript  
- Auto-reload using TSX  
- Clean folder structure  
- dotenv support  
- bcrypt ready  
- Easy scalability  
- Beginner friendly

---

## 📁 Folder Structure

project/
│
├── src/
│ └── server.ts
│
├── .gitignore
├── package.json
├── tsconfig.json
└── README.md


---

## 🛠️ Step 1: Initialize Project

```bash
npm init -y


This will create a package.json file.

🔹 Remove "type": "module"

If your package.json contains this:

"type": "module"


Remove it to avoid import/export conflicts.

🛠️ Step 2: Install Express
npm i express --save


Install Express TypeScript types:

npm i -D @types/express

🛠️ Step 3: Install TypeScript
npm i -D typescript


Create TypeScript config:

npx tsc --init

⚙️ tsconfig.json Configuration
✔️ 1) Comment out rootDir and outDir
 // "rootDir": "./src",
 // "outDir": "./dist",

✔️ 2) Comment out unnecessary output options
 // "sourceMap": true,
 // "declaration": true,

✔️ 3) From Recommendation options, comment out:
 // "jsx": "preserve",
 // "verbatimModuleSyntax": true,

🛠️ Step 4: Install TSX (Auto Reload for TypeScript)
npm i -D tsx


TSX will run .ts files directly with auto-reload support.

🛠️ Step 5: Create Your First Server

Create file: src/server.ts

import express, { Request, Response } from "express";

const app = express();
const port = 3000;

app.use(express.json());

app.get("/", (req: Request, res: Response) => {
  res.send("Hello from Express + TypeScript + TSX!");
});

app.listen(port, () => {
  console.log(`Server is running at http://localhost:${port}`);
});

🛠️ Step 6: Add Dev Script

Inside package.json → "scripts":

"scripts": {
  "dev": "tsx watch ./src/server.ts"
}


Run development server:

npm run dev

🌿 Using dotenv (Environment Variables)
Install dotenv
npm i dotenv


Create .env file:

PORT=5000


Update server.ts:

import "dotenv/config";

const port = process.env.PORT || 3000;

🔐 Using bcrypt (Password Hashing)
Install bcrypt
npm i bcrypt
npm i -D @types/bcrypt

Usage example
import bcrypt from "bcrypt";

const hashPassword = async (password: string) => {
  return await bcrypt.hash(password, 10);
};

const comparePassword = async (plain: string, hashed: string) => {
  return await bcrypt.compare(plain, hashed);
};

▶️ Run the Project
Development Mode
npm run dev


TSX will auto-restart the server on file changes.