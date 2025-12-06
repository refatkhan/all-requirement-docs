<div align="center">
  <h1>🚀 Express + TypeScript Starter Guide</h1>
  <h3><i>Complete Bangla Documentation for Beginners</i></h3>
</div>

<br/>

<div>
  <p>
    Express.js এবং TypeScript একসাথে ব্যবহার করলে প্রোজেক্ট আরও শক্তিশালী, নিরাপদ এবং Maintainable হয়।  
    এই গাইডে তুমি শিখবে—
  </p>

  <ul>
    <li>Express + TypeScript সার্ভার সেটআপ</li>
    <li>dotenv, bcrypt, cors, jwt এর ব্যবহার</li>
    <li>tsconfig.json এর important সেটিং</li>
    <li>Scripts & Folder Structure</li>
  </ul>
</div>

<hr/>

<section>
  <h2>🟦 ১) প্রোজেক্ট ইনিশিয়ালাইজ করা</h2>

  <pre><code>npm init -y</code></pre>

  <p>এতে একটি <code>package.json</code> তৈরি হবে।</p>

  <h3>🔹 "type" ফিল্ড কেন মুছবে?</h3>

  <pre><code>{
  "type": "module"
}</code></pre>

  <p>
    Express + TypeScript এর বেস সেটআপ সাধারণত CommonJS ভিত্তিক, তাই  
    <code>"type": "module"</code> থাকলে মুছে ফেলতে হবে।
  </p>
</section>

<hr/>

<section>
  <h2>🟦 ২) Express ইনস্টল করা</h2>

  <pre><code>npm install express</code></pre>
  <pre><code>npm install -D @types/express</code></pre>
</section>

<hr/>

<section>
  <h2>🟦 ৩) TypeScript ইনস্টল ও কনফিগার</h2>

  <pre><code>npm install -D typescript
npm install -D ts-node-dev @types/node</code></pre>

  <h3>🔹 tsconfig তৈরি</h3>

  <pre><code>npx tsc --init</code></pre>

  <h3>🔹 tsconfig প্রয়োজনীয় সেটিং</h3>

  <h4>✔️ rootDir & outDir সেট করো</h4>

  <pre><code>{
  "compilerOptions": {
    "rootDir": "./src",
    "outDir": "./dist"
  }
}</code></pre>

  <h4>✔️ অপ্রয়োজনীয় options কমেন্ট করো</h4>

  <pre><code>// "sourceMap": true,
// "declaration": true</code></pre>

  <h4>✔️ jsx এবং verbatimModuleSyntax কমেন্ট করো</h4>

  <pre><code>// "jsx": "preserve",
// "verbatimModuleSyntax": true</code></pre>
</section>

<hr/>

<section>
  <h2>🟦 ৪) Folder Structure</h2>

  <pre><code>project/
 ├─ src/
 │   └─ index.ts
 ├─ package.json
 └─ tsconfig.json
</code></pre>
</section>

<hr/>

<section>
  <h2>🟦 ৫) Express + TypeScript সার্ভার</h2>

  <pre><code>import express, { Request, Response } from "express";

const app = express();
const port = 3000;

app.use(express.json());

app.get("/", (req: Request, res: Response) => {
  res.send("Hello TypeScript + Express!");
});

app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
</code></pre>

  <p>➡️ ডেভেলপমেন্ট: ts-node-dev</p>
  <p>➡️ প্রডাকশন: tsc + node</p>
</section>

<hr/>

<section>
  <h2>🟦 ৬) package.json Scripts</h2>

<pre><code>{
 "scripts": {
  "dev": "ts-node-dev --respawn --transpile-only src/index.ts",
  "build": "tsc",
  "start": "node dist/index.js"
 }
}
</code></pre>

<h3>▶️ Development:</h3>
<pre><code>npm run dev</code></pre>

<h3>▶️ Production:</h3>
<pre><code>npm run build
npm start
</code></pre>
</section>

<hr/>

<section>
<h2>🟦 ৭) dotenv — Environment Variables</h2>

<h3>ইনস্টল</h3>
<pre><code>npm install dotenv</code></pre>

<h3>.env ফাইল:</h3>
<pre><code>PORT=5000
JWT_SECRET=secret
DB_URL=mongodb://...
</code></pre>

<h3>ব্যবহার</h3>
<pre><code>import "dotenv/config";
const port = process.env.PORT || 3000;
</code></pre>

</section>

<hr/>

<section>
<h2>🟦 ৮) bcrypt — Password Hashing</h2>

<h3>ইনস্টল:</h3>
<pre><code>npm install bcrypt
npm install -D @types/bcrypt
</code></pre>

<h3>Hash + Compare:</h3>
<pre><code>import bcrypt from "bcrypt";

export async function hashPassword(pass) {
  return bcrypt.hash(pass, 10);
}

export async function comparePassword(plain, hashed) {
  return bcrypt.compare(plain, hashed);
}
</code></pre>
</section>

<hr/>

<section>
<h2>🟦 ৯) অন্যান্য দরকারি ডিপেনডেন্সি</h2>

<h3>✔️ cors</h3>
<pre><code>npm install cors
npm install -D @types/cors
</code></pre>

<h3>✔️ morgan</h3>
<pre><code>npm install morgan
npm install -D @types/morgan
</code></pre>

<h3>✔️ jsonwebtoken</h3>
<pre><code>npm install jsonwebtoken
npm install -D @types/jsonwebtoken
</code></pre>
</section>

<hr/>

<section>
<h2>📝 Quick Recap</h2>

<ul>
  <li>npm init -y</li>
  <li>Install express + types</li>
  <li>Install TypeScript + ts-node-dev</li>
  <li>Setup tsconfig</li>
  <li>Create basic server</li>
  <li>Add dev/build/start scripts</li>
  <li>Setup dotenv + bcrypt</li>
  <li>Use cors / morgan / jwt when needed</li>
</ul>
</section>

<br/>

