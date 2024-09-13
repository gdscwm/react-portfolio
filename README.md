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

If `/usr/local/bin` is missing from the output, add it to your `$PATH` by editing your `~/.zprofile` file and adding the following line:

```bash
export PATH=/usr/local/bin:$PATH
```

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

## Start the project

Run the following command to start the project.

```bash
npm run dev
```

This will start a local development server at port 3000 by default. In simpler terms, this will be a local version of your portfolio website that will change with your files and let you see what the website looks like in real-time. Your portfolio website can be accessed at http://localhost:3000.

**Tip:** Split your windows between your code editor/IDE and the local development server to see real-time updates.
