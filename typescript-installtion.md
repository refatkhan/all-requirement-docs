<div align="center">
  <h1>🚀 Express + TypeScript Starter Guide</h1>
  <h3><i>Complete English Documentation for Beginners</i></h3>
</div>

<br/>

<div>
  <p>
    Using Express.js together with TypeScript makes your project more powerful, secure, and maintainable.  
    In this guide, you will learn—
  </p>

  <ul>
    <li>How to set up an Express + TypeScript server</li>
    <li>How to use dotenv, bcrypt, cors, and jwt</li>
    <li>Important tsconfig.json settings</li>
    <li>Scripts & Folder Structure</li>
  </ul>
</div>

<hr/>

<section>
  <h2>🟦 1) Initialize the Project</h2>

  <pre><code>npm init -y</code></pre>

  <p>This will create a <code>package.json</code> file.</p>

  <h3>🔹 Why remove the "type" field?</h3>

  <pre><code>{
  "type": "module"
}</code></pre>

  <p>
    The basic Express + TypeScript setup is usually based on CommonJS,  
    so if <code>"type": "module"</code> exists, it should be removed.
  </p>
</section>

<hr/>

<section>
  <h2>🟦 2) Install Express</h2>

  <pre><code>npm install express</code></pre>
  <pre><code>npm install -D @types/express</code></pre>
</section>

<hr/>

<section>
  <h2>🟦 3) Install & Configure TypeScript</h2>

  <pre><code>npm install -D typescript
npm install -D ts-node-dev @types/node</code></pre>

  <h3>🔹 Create tsconfig</h3>

  <pre><code>npx tsc --init</code></pre>

  <h3>🔹 Required tsconfig settings</h3>

  <h4>✔️ Set rootDir & outDir</h4>

  <pre><code>{
  "compilerOptions": {
    "rootDir": "./src",
    "outDir": "./dist"
  }
}</code></pre>

  <h4>✔️ Comment unnecessary options</h4>

  <pre><code>// "sourceMap": true,
// "declaration": true</code></pre>

  <h4>✔️ Comment jsx and verbatimModuleSyntax</h4>

  <pre><code>// "jsx": "preserve",
// "verbatimModuleSyntax": true</code></pre>
</section>

<hr/>

<section>
  <h2>🟦 4) Folder Structure</h2>

  <pre><code>project/
 ├─ src/
 │   └─ index.ts
 ├─ package.json
 └─ tsconfig.json
</code></pre>
</section>

<hr/>

<section>
  <h2>🟦 5) Express + TypeScript Server</h2>

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

  <p>➡️ Development: ts-node-dev</p>
  <p>➡️ Production: tsc + node</p>
</section>

<hr/>

<section>
  <h2>🟦 6) package.json Scripts</h2>

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
<h2>🟦 7) dotenv — Environment Variables</h2>

<h3>Install</h3>
<pre><code>npm install dotenv</code></pre>

<h3>.env file:</h3>
<pre><code>PORT=5000
JWT_SECRET=secret
DB_URL=mongodb://...
</code></pre>

<h3>Usage</h3>
<pre><code>import "dotenv/config";
const port = process.env.PORT || 3000;
</code></pre>

</section>

<hr/>

<section>
<h2>🟦 8) bcrypt — Password Hashing</h2>

<h3>Install:</h3>
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
<h2>🟦 9) Other Useful Dependencies</h2>

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
  <li>Set up tsconfig</li>
  <li>Create a basic server</li>
  <li>Add dev/build/start scripts</li>
  <li>Set up dotenv + bcrypt</li>
  <li>Use cors / morgan / jwt when needed</li>
</ul>
</section>

<br/>

<div align="center">
  <h2>🎉 You're Now Ready!</h2>
  <p>If you want, I can create a <b>full modular boilerplate (routes + controllers + services)</b> for you using this setup.</p>
</div>
