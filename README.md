# GDSC Fall 2024 Workshop #3: Building a Portfolio Website

In this workshop, we will be using the following technologies to build a portfolio web application:

- **React**: A UI library that provides APIs for attaching UI components to the Document Object Model (DOM) and utilizing features like state management and rendering algorithms.
- **Next.js**: A React framework that allows you to build React apps by providing the features that React is missing out of the box, such as a router, data fetching, server-side rendering, and bundling.
- **Tailwind CSS**: A CSS framework with a "utility-first" approach, designed for fast development and easy maintenance, that integrates well with component-based UI frameworks like React.

## Prerequisites

### Install Node.js

Make sure you have Node.js (and by extension, Next.js) installed. Check your versions with the following commands:

```bash
node --version
npx next --version
```

If Node.js is not installed, download it from Node.js official website here: https://nodejs.org/en. After installation, verify that `/usr/local/bin` is in your `$PATH`:


```bash
echo $PATH
```

To add a variable to your path in Windows:

   Right-click on the Start Button

   Select “System” from the context menu.

   Click “Advanced system settings”

   Go to the “Advanced” tab

   Click “Environment Variables…”

   Click variable called “Path” and click “Edit…”

   Click “New” and add the folder you extracted. The directory is probabaly: C:\Program Files\nodejs\bin

Mac/Linux:
If `/usr/local/bin` is missing from the output, add it to your `$PATH` by editing your `~/.zprofile` file and adding the following line:

```bash
export PATH=/usr/local/bin:$PATH
```

if on M1/M2 Mac run ```export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm```

### Start Next.js app

If you have a directory for workshops, navigate there. If not, then create a new directory for your workshops:
```bash
mkdir gdsc-workshops
```

Navigate to that directory, then start a new Next.js app by running:

```bash
npx create-next-app@latest
```

On installation, you'll see the following prompts. Respond to all (we recommend you choose the default values):
What is your project named? portfolio
Would you like to use TypeScript? Yes
Would you like to use ESLint? Yes
Would you like to use Tailwind CSS? Yes
Would you like your code inside a src/ directory? No
Would you like to use App Router? (recommended) Yes
Would you like to use Turbopack for next dev? No
Would you like to customize the import alias (@/* by default)? No

After the prompts, `create-next-app` will create a new folder with your project name and install the necessary dependencies.


### Install Tailwind CSS

Install Tailwind CSS via `npm` and create the configuration file:

```bash
npm install -D tailwindcss
npx tailwindcss init
```

We create our own configuration file in case we want to customize our media query breakpoints, add custom colors or fonts, or otherwise fine-tune our Tailwind CSS configuration later.


### Grab images

Ensure you are not within the `react-portfolio` project directory. Once you have, to clone the images you need for this project, go to the GitHub repository and click the green `Code` button. Clone using the web URL (HTTPS) with this command:

```bash
git clone <repository-url>
```

There should just be one folder called `public`. Move this one folder into your `react-portfolio` project directory. The easiest way to do this is via file explorer by dragging the folder into your project directory, then returning to your project folder in the command line and deleting the cloned repository manually.

### Start server

Run the following command to start the project.

```bash
npm run dev
```

This will start a local development server at port 3000 by default. In simpler terms, this will be a local version of your portfolio website that will change with your files and let you see what the website looks like in real-time. Your portfolio website can be accessed at http://localhost:3000.

**Tip:** Split your windows between your code editor/IDE and the local development server to see real-time updates.


## Begin coding

Before we begin building this portfolio, let's download some React icons for later. Run the following command:

```bash
npm i react-icons
````

From the sidebar, look for the `app` folder. Inside the app folder, find and open up the `page.tsx` file. After you clear away all the existing content, write the following lines of code.

```bash

// Type definition that helps manage metadata
import type { Metadata } from 'next'
 
// Defines some metadata, e.g. sets title
export const metadata: Metadata = {
  title: 'My Portfolio',
}
 
// Creates functional component Page
export default function Page() {
  return (
    <div>
      <>
        <title>My Portfolio</title>
        <meta name="description" content="Generated by create-next-app" />
        <link rel="icon" href="/favicon.ico" />
      </>
      <main></main>
    </div>
  );
}
```

One thing we need to do to get Tailwind working is to open up `globals.css` file and add some changes.

Remove this entire block of code (since we will later use Tailwind to make our own)

```bash

@media (prefers-color-scheme: dark) {
  :root {
    --background: #0a0a0a;
    --foreground: #ededed;
}
```

Then, add the following lines of code to the top of the `globals.css` file to include all the neccessary classes and components for Tailwind.

```bash
@tailwind base;
@tailwind components;
@tailwind utilities;
```

We can also customize the font by including this code after the previous classes.

```bash
@font-face {
    font-family: 'burtons';
    src: url('../public/Burtons.otf');
}
```


<hr/>


# More information

This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.
