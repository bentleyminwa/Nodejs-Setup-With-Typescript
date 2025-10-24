# TypeScript in a Node.js Project

## Setup Node.js Project

First, dedicate a folder for your project. Open the terminal, I highly suggest bash😉 for reasons you'll figure out. Run the following commands:

```
// Command Line
mkdir node-ts-project && cd node-ts-project
npm init -y
```

Now, let's break down what each command does, shall we😌:

- mkdir node-ts-project && cd node-ts-project: Creates a new project directory called node-ts-project and moves into that directory.
- npm init -y: Initializes a new package.json file with default values.

The package.json file is essential for any Node.js project, as it's responsible for managing dependencies and scripts for your project. Its importance is kinda underrated🥲.

## TypeScript in Node.js

Let's now install TypeScript as a dev dependency and create a configuration file:

```
// Command Line
npm install --save-dev typescript
touch tsconfig.json
```

As always, let's break down what each command does:
- npm install --save-dev typescript: Installs ts locally for your project.
- touch tsconfig.json: Creates a TypeScript configuration file.

Speaking of the configuration file, let's go ahead and add the following configurations to your tsconfig.json file:

```
// tsconfig.json
{
  "compilerOptions": {
    /* Modern JavaScript & Browser Compatibility: */
    "target": "ESNext", // Uses the latest ECMAScript features for modern JavaScript support

    /* Module System Settings: */
    "module": "NodeNext", // Configures Node.js to use ESM module system
    "rootDir": "src", // Specifies the source directory for your code
    "outDir": "dist", // Specifies the output directory for compiled files
    "sourceMap": true, // Enables source maps for easier debugging

    /* Module Resolution Strategy: */
    "moduleResolution": "NodeNext", // Resolves modules using Node’s ESM strategy
    "moduleDetection": "force", // Forces TypeScript to treat files as modules

    /* Interoperability and File Consistency: */
    "esModuleInterop": true, // Ensures compatibility between CommonJS and ESM modules
    "forceConsistentCasingInFileNames": true, // Prevents case-sensitivity issues across platforms

    /* Strict Type-Checking: */
    "strict": true, // Enables strict type-checking for fewer runtime errors
    "noUncheckedIndexedAccess": true, // Enforces type safety for array/object accesses
    "noImplicitOverride": true, // Enforces explicit use of `override` for methods overriding base class methods
    "noImplicitAny": true, // Prevents the use of `any` type unless explicitly defined
    "skipLibCheck": true, // Skips type-checking of declaration files for faster compilation
    "resolveJsonModule": true, // Allows importing JSON files as modules
    "declaration": true, // Generates `.d.ts` files for type definitions
    "allowSyntheticDefaultImports": true, // Allows default imports for CommonJS modules
    "allowImportingTsExtensions": true, // Allows importing `.ts` files with their extensions
    "verbatimModuleSyntax": true, // Keeps the `import`/`export` syntax as-is without transformation

    // Include modern ECMAScript (ES2022) and DOM APIs for frontend
    "lib": ["ES2022", "DOM"] // Include ES2022 features and DOM APIs for frontend development
    // Uncomment this for backend code without DOM APIs
    /* "lib": ["ES2022"] */
  },
  "include": ["src"], // Includes the `src` directory in the project
  "exclude": ["node_modules", "dist"] // Excludes `node_modules` and `dist` directories from the project
}
```

Optionally, add the following lines for JavaScript support in a TypeScript project:

```
// tsconfig.json
{
  "compilerOptions": {
    ...
    "allowJs": true,
    "checkJs": true
  }
}
```

Since we are fully committing to ESM(I don't know why we wouldn't👀), add this to the package.json:

```
// package.json
{
  "type": "module"
}
```

## Source Folder and Entry File

Create a src folder and an index.ts file inside it:

```
// Command Line
mkdir src
touch src/index.ts
```

Add a simple TypeScript script in src/index.ts:

```
// src/index.ts
console.log('Hello world!');
```

Of course, the infamous Hello World. This will serve as our starting point to ensure everything is working correctly.

## Run & Compile Typescript Files in Node.js

To run TypeScript files directly without compiling them first, install tsx, which is a popular TypeScript runner. An alternative would be to use ts-node:

```
// Command Line
npm install tsx --save-dev
```

Now update your package.json scripts to use tsx:

```
// package.json
"scripts": {
  "dev": "tsx src/index.ts",
  "build": "tsc",
  "start": "node dist/index.js"
}
```

Again, as always, let's break down what each script does:
- "dev": "tsx --watch src/index.ts": Runs the project in development mode using tsx. The --watch flag makes tsx automatically recompile and reload files when changes are made.
- "build": "tsc": Compiles TypeScript files into JavaScript using the TypeScript compiler (tsc). The compiled files are stored in the dist folder.
- "start": "node dist/index.js": Runs the compiled JavaScript files in production mode.

## Environment Variables in Node.js

Many applications require sensitive API keys and environment variables. The best practice is to store them in a .env file instead of hardcoding them. Create a .env file in your project directory with the following content:

```
# .env
YOUR_API_KEY="sk-proj-123abc"
```

To ensure environment variables are recognized by TypeScript, install Node.js type definitions:

```
// Command Line
npm install @types/node --save-dev
```

If you're using Node.js version 20.6.0 or newer, you can load environment variables directly using the --env-file flag:

```
// package.json
"scripts": {
  "dev": "tsx --watch --env-file=.env src/index.ts",
  "build": "tsc",
  "start": "node --env-file=.env dist/index.js"
}
```

For a more familiar and sophisticated approach, let's consider using the dotenv package:

```
// Command Line
npm install dotenv
```

Then let's modify src/index.ts to load the .env file using dotenv:

```
// src/index.ts
import "dotenv/config";

console.log(process.env.YOUR_API_KEY);
```

Now update the package.json scripts accordingly:

```
// package.json
"scripts": {
  "dev": "tsx --watch src/index.ts",
  "build": "tsc",
  "start": "node dist/index.js"
}
```

Now, your project can surely read environment variables.

See! Setting up a TypeScript project with Node.js wasn't as hard as you thought😉.
