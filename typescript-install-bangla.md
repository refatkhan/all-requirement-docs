# 🚀 Express + TypeScript Basic Server Setup (Bangla Guide)

এখানে দেখানো হলো কীভাবে প্রথমবার Express + TypeScript ব্যবহার করে একটি বেসিক সার্ভার সেটআপ করতে হয়, কেন কোন ডিপেনডেন্সি লাগে, আর কীভাবে এগুলো কাজ করে।

---

## 🟦 ১) প্রোজেক্ট ইনিশিয়ালাইজ করা

প্রথমে একটা ফোল্ডার নাও, তারপর টার্মিনালে লিখো:

```bash
npm init -y
এতে তোমার প্রোজেক্টে একটি package.json তৈরি হবে।

🔹 "type" ফিল্ড কেন মুছবে?
অনেক সময় নতুন প্রোজেক্টে package.json এ থাকে:

json
Copy code
{
  "type": "module"
}
আমরা TypeScript + Express-এর বেসিক সেটআপে সাধারণত CommonJS ব্যবহার করি (মানে require / module.exports সিস্টেম, যেটা কম্পাইল হওয়া জাভাস্ক্রিপ্টেও কাজ করে)।

➡️ তাই "type": "module" লাইনটা থাকলে মুছে দাও।

এতে Node ডিফল্টভাবে CommonJS ধরে নেবে, আর TypeScript থেকে কম্পাইল হওয়া কোড ঠিকভাবে রান করবে।

🟦 ২) Express ইনস্টল করা
bash
Copy code
npm i express --save
--save মানে এটা dependencies সেকশনে যাবে এবং প্রডাকশনে লাগবে।

TypeScript এর সাথে ব্যবহার করার জন্য Express-এর টাইপ দরকার:

bash
Copy code
npm i -D @types/express
এটা devDependencies এ থাকবে, কারণ শুধু টাইপ চেক করার সময় লাগে।

🟦 ৩) TypeScript ইনস্টল ও কনফিগার করা
🔹 TypeScript ইনস্টল
bash
Copy code
npm i -D typescript
আরও সুবিধার জন্য এগুলো ইনস্টল করো:

bash
Copy code
npm i -D ts-node-dev @types/node
typescript → Type check + JS এ কম্পাইল করে

ts-node-dev → .ts ফাইল সরাসরি রান + auto reload

@types/node → Node.js এর টাইপ ডেফিনিশন

🔹 tsconfig তৈরি করা
bash
Copy code
npx tsc --init
এতে tsconfig.json ফাইল তৈরি হবে।

⚙️ tsconfig এ দরকারি সেটিং
✔️ ১) rootDir এবং outDir সেট করা (Better Practice)
jsonc
Copy code
{
  "compilerOptions": {
    "rootDir": "./src",
    "outDir": "./dist"
  }
}
যদিও তুমি প্রথমে কমেন্ট রাখার কথা বলেছিলে,
কিন্তু প্রফেশনাল প্রোজেক্টে এগুলো ঠিক করে সেট রাখাই ভালো।

✔️ ২) Output অপশনগুলো কমেন্ট রাখা
json
Copy code
// "sourceMap": true,
// "declaration": true
✔️ ৩) Recommendation অপশন কমেন্ট করা
json
Copy code
// "jsx": "preserve",
// "verbatimModuleSyntax": true
React বা JSX না থাকলে এগুলো লাগবে না।

🟦 ৪) ফোল্ডার স্ট্রাকচার
pgsql
Copy code
project-folder/
 ├─ src/
 │   └─ index.ts
 ├─ package.json
 └─ tsconfig.json
🟦 ৫) প্রথম Express + TypeScript সার্ভার
src/index.ts ফাইল তৈরি করো:

ts
Copy code
import express, { Request, Response } from "express";

const app = express();
const port = 3000;

// JSON body parse করার জন্য
app.use(express.json());

app.get("/", (req: Request, res: Response) => {
  res.send("Hello TypeScript + Express!");
});

app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
এখন সার্ভার চালানোর ২টি উপায়:
✔️ ডেভেলপমেন্ট:
ts-node-dev দিয়ে .ts ফাইল সরাসরি রান হবে, auto reload হবে।

✔️ প্রডাকশন:
TypeScript → JavaScript বানানো হবে, তারপর Node দিয়ে রান।

🟦 ৬) package.json এ স্ক্রিপ্ট সেট করা
json
Copy code
"scripts": {
  "dev": "ts-node-dev --respawn --transpile-only src/index.ts",
  "build": "tsc",
  "start": "node dist/index.js"
}
✔️ ডেভেলপমেন্ট রান:
bash
Copy code
npm run dev
✔️ প্রডাকশন বিল্ড:
bash
Copy code
npm run build
npm start
🟦 ৭) dotenv — কখন লাগবে, কীভাবে কাজ করে?
✔️ কখন ব্যবহার করবে?
যখন দরকার:

Database URL

JWT Secret

API Keys

Custom PORT

তখন .env ফাইলে রাখতে হবে।

🔹 ইনস্টল
bash
Copy code
npm i dotenv
🔹 ব্যবহার
.env তৈরি:

ini
Copy code
PORT=5000
JWT_SECRET=my-secret
DB_URL=mongodb://...
src/index.ts এ:

ts
Copy code
import "dotenv/config";

const port = process.env.PORT || 3000;
কী করছে?
.env থেকে সব ভ্যালু process.env এর ভিতরে সেট করে

এগুলো কোডের বাইরে থাকে → secure configuration

🟦 ৮) bcrypt — কেন লাগবে, কখন লাগবে?
✔️ কেন?
Password কখনো plain text হিসেবে ডাটাবেজে রাখা যাবে না।

তাই bcrypt দিয়ে hash করতে হবে:

Register → Hash save

Login → bcrypt.compare দিয়ে মিলানো

🔹 ইনস্টল
bash
Copy code
npm i bcrypt
npm i -D @types/bcrypt
🔹 Hash + Compare উদাহরণ:
ts
Copy code
import bcrypt from "bcrypt";

const SALT_ROUNDS = 10;

export async function hashPassword(plainPassword: string): Promise<string> {
  return await bcrypt.hash(plainPassword, SALT_ROUNDS);
}

export async function comparePassword(
  plainPassword: string,
  hashedPassword: string
): Promise<boolean> {
  return await bcrypt.compare(plainPassword, hashedPassword);
}
🟦 ৯) অন্য দরকারি ডিপেনডেন্সি
✔️ cors
React → Express ভিন্ন origin হলে লাগবে:

bash
Copy code
npm i cors
npm i -D @types/cors
Usage:

ts
Copy code
import cors from "cors";
app.use(cors());
✔️ morgan (logging)
bash
Copy code
npm i morgan
npm i -D @types/morgan
ts
Copy code
import morgan from "morgan";
app.use(morgan("dev"));
✔️ jsonwebtoken (JWT auth)
bash
Copy code
npm i jsonwebtoken
npm i -D @types/jsonwebtoken
Access + Refresh token বানাতে ব্যবহৃত হয়।