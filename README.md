# GDSC Fall 2024 Workshop Series: Building a Portfolio Website

In this workshop, we will be using the following technologies to build a portfolio web application:

- **React**: A UI library that provides APIs for attaching UI components to the Document Object Model (DOM) and utilizing features like state management and rendering algorithms.
- **Next.js**: A React framework that allows you to build React apps by providing the features that React is missing out of the box, such as a router, data fetching, server-side rendering, and bundling.
- **Tailwind CSS**: A CSS framework with a "utility-first" approach, designed for fast development and easy maintenance, that integrates well with component-based UI frameworks like React.

For a more thorough breakdown of these technologies, watch the following brief videos:
- [React in 100 seconds](https://www.youtube.com/watch?v=mr15Xzb1Ook)
- [Tailwind in 100 seconds](https://www.youtube.com/watch?v=Tn6-PIqc4UM)

## Prerequisites

### Install npm

#### Checking your version of npm and Node.js

To see if you already have Node.js (and by extension, Next.js) and npm installed and to check the installed version, run the following commands:

```bash
node -v
npm -v
npx next --version
```

#### Using a Node package manager to install Node.js and npm

If you don't have Node.js adn npm installed, you can use a Node installer to install both Node.js and npm on your system.

- [Node.js installer](https://nodejs.org/en/download/package-manager)
- [NodeSource installer](https://github.com/nodesource/distributions)

If you use Linux, we recommend that you use a NodeSource installer.

##### OS X or Windows Node installers

If you're using OS X or Windows, use one of the installers from the [Node.js download page](https://nodejs.org/en/download/). Make sure to install the version labeled LTS.

##### Linux or other operating systems Node installers

If you're using Linux or another operating system, use one of the following installers:

- [NodeSource installer](https://github.com/nodesource/distributions) (recommended)
- One of the installers on the [Node.js download page](https://nodejs.org/en/download/)
- Or see [this page](https://nodejs.org/en/download/package-manager/) to install npm for Linux in the way many Linux developers prefer.

Make sure you have Node.js (and by extension, Next.js) installed. Check your versions with the following commands:

#### Using a prebuilt installer to install Node.js and npm

If you're unable or uncomfortable with installing Node.js and npm from the command line, feel free to use the prebuilt to download Node.js to your laptop [here](https://nodejs.org/en/download/prebuilt-installer).

### Check that you can use Node.js and npm from the command line

After installation, verify that `/usr/local/bin` is in your `$PATH`:

```bash
echo $PATH
```

If `/usr/local/bin` is missing from the output, add it to your `$PATH` by editing your `~/.zprofile` file and adding the following line:

```bash
export PATH=/usr/local/bin:$PATH
```

### Start Next.js app

If you have a directory for workshops, navigate there using the command `cd`. If not, then create a new directory for your workshops:
```bash
mkdir gdsc-workshops
```

Navigate to that directory, then start a new Next.js app by running:

```bash
npx create-next-app@latest
```

On installation, you'll see the following prompts. Respond to all (we recommend you choose the default values):

```bash
What is your project named? portfolio
Would you like to use TypeScript? Yes
Would you like to use ESLint? Yes
Would you like to use Tailwind CSS? Yes
Would you like your code inside a src/ directory? No
Would you like to use App Router? (recommended) Yes
Would you like to use Turbopack for next dev? No
Would you like to customize the import alias (@/* by default)? No
```

After the prompts, `create-next-app` will create a new folder with your project name and install the necessary dependencies.

> **Tip:** For a faster process, simply run `npx create-next-app@latest portfolio --typescript --eslint --tailwind` and answer the following prompts with the recommended default values:
> ```bash
> Would you like your code inside a src/ directory? No
> Would you like to use App Router? (recommended) Yes
> Would you like to customize the import alias (@/* by default)? No
> ```

### Install Tailwind CSS

Since we're using Tailwind with Next.js, reference [this documentation](https://tailwindcss.com/docs/guides/nextjs).

#### Install via `npm` and create the configuration file.

Here, we install Tailwind CSS and its peer dependencies via npm, and then run the init command to generate both `tailwind.config.js` and `postcss.config.js`.

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

We will create our own configuration file in case we want to customize our media query breakpoints, add custom colors or fonts, or otherwise fine-tune our Tailwind CSS configuration later.

#### Configure your template paths

Add the paths to all of your template files in your `tailwind.config.js` file. 

```js
module.exports = {
  content: [
    "./app/**/*.{js,ts,jsx,tsx,mdx}",
    "./pages/**/*.{js,ts,jsx,tsx,mdx}",
    "./components/**/*.{js,ts,jsx,tsx,mdx}",
],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Configuring the paths to all your content files tells Tailwind about every single file in your project that contains any Tailwind class names so that it can scan all your files for class names and generate all of the corresponding CSS for those styles.

### Grab images (optional)

Ensure you are not within the `react-portfolio` project directory. Once you have, to clone the images you need for this project, go to the GitHub repository and click the green `Code` button. Clone using the web URL (HTTPS) with this command:

```bash
git clone <repository-url>
```

There should just be one folder called `public`. Move this one folder into your `react-portfolio` project directory. 

The easiest way to do this is via file explorer by dragging the folder into your project directory, then returning to your project folder in the command line and deleting the cloned repository manually.

### Start server

Run the following command to start the project.

```bash
npm run dev
```

This will start a local development server at port 3000 by default. In simpler terms, this will be a local version of your portfolio website that will change with your files and let you see what the website looks like in real-time. Your portfolio website can be accessed at http://localhost:3000.

**Tip:** Split your windows between your code editor/IDE and the local development server to see real-time updates.


## Some more setup

Before we begin building this portfolio, let's download some React icons for later. Run the following command:

```bash
npm i react-icons
````

If you're using VSCode as your code editor, now is the time to add the Tailwind CSS extension! 

> **Optional:** Simply go down the sidebar on the left until you're hovering over the Extensions icon, click the icon, and then search for "Tailwind." Install the first extension, which should be called "Tailwind CSS IntelliSense."

> To enable the autocomplete and linting features, click the gear icon, select "Extension Settings," and first search for "files.associations," which should have one item added with the item being `*.css` and the value being `tailwindcss`. This tells VSCode to always open `.css` files in Tailwind CSS mode.

> Second, search for "editor.quickSuggestions" and make sure the value for the item `strings` is `on`. This tells VSCode to trigger completions for string content, too.

Now, from the open project directory, look for the `app` folder. Inside the app folder, find and open up the `page.tsx` file. After you clear away all the existing content, write the following lines of code.

```js
// Type definition that helps manage metadata
import type { Metadata } from 'next'
 
// Defines some metadata, e.g. sets title
export const metadata: Metadata = {
  title: 'Kathy Rowe Portfolio',
}
 
// Creates functional component Page
export default function Page() {
  return (
    <div>
      <>
        <title>Kathy Rowe Portfolio</title>
        <meta name="description" content="Generated by create-next-app" />
        <link rel="icon" href="/favicon.ico" />
      </>
      <main></main>
    </div>
  );
}
```

One thing we need to do to get Tailwind working is to open up `globals.css` file and add some changes.

Remove this entire rule (since we will later use Tailwind to make our own media queries).

```js
@media (prefers-color-scheme: dark) {
  :root {
    --background: #0a0a0a;
    --foreground: #ededed;
}
```

Then, add the following lines of code to the top of the `globals.css` file to include all the neccessary classes and utilities to make our Tailwind code functional.

```js
@tailwind base;
@tailwind components;
@tailwind utilities;
```

# End of Workshop One.

<!-- We can also customize the font by including this code after the previous classes. This font should be stored within the `public` folder that you downloaded earlier.

```js
@font-face {
    font-family: 'burtons';
    src: url('../public/Burtons.otf');
}
``` -->

## Begin coding

### Creating the nav bar

We're going to start with a nav bar that contains a title, an icon for dark mode, and a button for your resume.

To do this, first import the icon for dark mode from the React icons package we previously downloaded at the top of the file.

```js
import { BsFillMoonStarsFill } from 'react-icons/bs';
```

Then, create a new `<section>` from within our `<main>` element to enclose the nav bar. Add the `nav` element with the new section and give it a title, which will be your full name. From within that nav bar, add a `<ul>` tag, which is where the dark mode icon and the button are going to go. We want the nav bar to fill up the page horizontally and for there to be some padding, so apply classes to style the elements on the page.

```js
<main className='bg-white px-10'>
  <section className='min-h-screen'>
    <nav className='py-10 mb-12 flex justify-between'>
      <h1 className='text-xl'>Kathy Rowe</h1>
      <ul className='flex items-center'>
        <li>
          <BsFillMoonStarsFill className='cursor-pointer text-2xl'/>
        </li>
        <li><a href='#'>Resume</a></li>
      </ul>
    </nav>
  </section>
</main>
```

**Tip:** One way to check if you have the Tailwind extension installed with the autocomplete and linting features enabled is to simply type out `className=''` and add a space between the quotes. There should be a list of utility classes that pop up as options.

But the Resume button is still unstyled and too close to the dark mode icon. Let's apply some styling and padding to the `<a`> tag to make it look more like a button, as well as a nice gradient. Add a link to your resume to the `href` attribute.

```js
<li>
 <a className='bg-gradient-to-r from-cyan-500 to-blue-600 text-white px-4 py-2 rounded-md ml-8' href='#'>
  Resume
 </a>
</li>
```

**Extra:** Here's some [examples of a good resume](https://www.overleaf.com/latex/templates/jakes-resume/syzfjbzwjncs) to keep in mind.

<!-- Return to your `tailwind.config.js` file and add the custom font family you downloaded to the theme. 

```js
theme: {
  extend: {
    fontFamily: {
      burtons: 'burtons'
    },
  },
},
```

Now, we can apply our custom font to the title of the nav bar we just made, which should be your name.

```bash
<h1 className='text-xl font-burtons'>Kathy Rowe</h1>
```
-->

### Creating the main page

Let's move on to the main page. Under the `nav` element, create a new `div`. This will be the container for everything within this section.

```js
<div className='flex justify-center items-center h-[65vh]'></div>
```

The classes above just ensure that everything is centered perfectly, both vertically and horizontally.

Then, start another `div` within in and include your full name, your most recent role, and some (brief!) background on what you do.

```js
<div>
  <h2>Kathy Rowe</h2>
  <h3>28th President of William & Mary.</h3>
  <p>Nationally recognized as an innovator in higher education, I champion the liberal arts, 
    entrepreneurship and strengthening education-workforce pathways.</p>
</div>
```

Let's add some buttons with icons represented the various ways someone could contact you. Write out the following import statement at the top of this file.

```js
import { 
  AiFillLinkedin, 
  AiFillTwitterCircle, 
  AiFillMail,
  AiFillGithub
} from 'react-icons/ai';
```

Start another `div` and add those icons to `<a>` tags to create clickable icons linking to your various social media platforms.

```js
<div>
  <a href='https://www.linkedin.com/in/katherine-rowe-2a711545'><AiFillLinkedin /></a>
  <a href='https://x.com/williamandmary'><AiFillTwitterCircle /></a>
  <a href='https://www.github.com/gdscwm'><AiFillGithub /></a>
  <a href='mailto:president@wm.edu'><AiFillMessage /></a>
</div>
```

Now, let's add some styling!

```js
<div className='text-left p-10'>
  <h2 className='text-xl py-2 text-blue-600 font-bold'>KATHY ROWE</h2>
  <h3 className='text-3xl py-2 font-bold text-gray-700'>28th President of William & Mary 👋</h3>
  <p className='text-md py-5 text-gray-800'>
    Nationally recognized as an innovator in higher education, <br />
    I champion the liberal arts, entrepreneurship and <br />
    strengthening education-workforce pathways. <br />
  </p>
  <div className='text-5xl flex justify-center gap-16 py-3 text-gray-800'>
    <a href='https://www.linkedin.com/in/katherine-rowe-2a711545'><AiFillLinkedin /></a>
    <a href='https://x.com/williamandmary'><AiFillTwitterCircle /></a>
    <a href='https://www.github.com/gdscwm'><AiFillGithub /></a>
    <a href='mailto:president@wm.edu'><AiFillMail /></a>
  </div>
</div>
```

For our next step, you are going to import an image of yourself (preferably a professional headshot, but any well-lit image will do), so you will need to upload that image to the `public` folder, then import both the `Image` component and your image at the top of the file.

```js
import Image from 'next/image';
import kathy from '../public/kathy.jpg';
```

Then, start a new `div` and add an `Image` component with the `src` as the image you imported.

```js
<div className='mx-auto bg-gradient-to-b from-teal-500 to-white rounded-full w-80 h-80 mt-20'>
  <Image src={kathy} alt='profile_pic'/>
</div>
```

But now this image isn't _quite_ centered properly. Let's fix that with some styling.

```js
<div className='relative mx-auto bg-gradient-to-b from-teal-500 to-white rounded-full w-80 h-80 mt-20 overflow-hidden'>
  <Image src={kathy} alt='profile_pic' layout='fill' objectFit='cover'/>
</div>
```

There we go!

This will ensure that your image is centered and styled correctly. The `relative` and `overflow-hidden` classes help keep your image properly framed within the rounded container.

Before we move on, let's check that this is our final product.

```js
<div className='flex justify-center items-center h-[65vh]'>
  <div className='text-left p-10'>
    <h2 className='text-xl py-2 text-blue-600 font-bold'>KATHY ROWE</h2>
    <h3 className='text-3xl py-2 font-bold text-gray-700'>28th President of William & Mary 👋</h3>
    <p className='text-md py-5 text-gray-800'>
      Nationally recognized as an innovator in higher education, <br />
      I champion the liberal arts, entrepreneurship and <br />
      strengthening education-workforce pathways. <br />
    </p>
    <div className='text-5xl flex justify-center gap-16 py-3 text-gray-800'>
      <a href='https://www.linkedin.com/in/katherine-rowe-2a711545'><AiFillLinkedin /></a>
      <a href='https://x.com/williamandmary'><AiFillTwitterCircle /></a>
      <a href='https://www.github.com/gdscwm'><AiFillGithub /></a>
      <a href='mailto:president@wm.edu'><AiFillMail /></a>
    </div>
  </div>
  <div className="bg-gradient-to-b from-blue-600 rounded-full w-80 h-80 relative overflow-hidden">
    <Image src={kathy} alt='profile_pic' layout="fill" objectFit="cover" />
  </div>
</div>
```
# End of Workshop Two.

### Creating the education page

Now that you have the main page done, let's move on to the second section! This will be where you put all your education, which should include college (and high school if you are a freshmen or sophomore).

Start off with creating a new `section`. This will serve as the container holding all the elements we use for this page.

```js
<section>
  <div>
    <h3>EDUCATION</h3>
  </div>
</section>
```

Next, add these styling classes.

```js
<section className='flex justify-center items-center'>
  <div className='flex flex-col items-start space-y-4 p-6 bg-white rounded-lg w-full max-w-4xl'>
    <h3 className='text-lg text-blue-600 font-bold'>EDUCATION</h3>
  </div>
</section>
```

Now, we have a title, but nothing else. Let's add the schools you went to and which years you went to them as text, using the `<p>` tag. 

The following code should be placed after the heading (this line: `<h3 className='text-lg text-blue-600 font-bold'>EDUCATION</h3>`).

```js
<div className='flex justify-between w-full h-auto'>
  <p className='text-lg font-semibold'>
    College of William and Mary
  </p>
  <p className='text-sm text-gray-800 font-bold text-right'>
    MAY 2026
  </p>
</div>
```

But this text looks a little lonely... why don't we put some more information? For example, like your major(s)/minor and any classes relevant to your desired career.

If you haven't declared a major yet, you can put down whichever major(s) you're most strongly considering, or the major(s) that you applied with.

<hr/>


### Creating the experience page

Now that you have the education page done, let's move on to the third section! This will be where you put all your experience.

To make things faster, simply copy over the Education section here and remove all of the text specific to that section. Here's an example of what that might look like.

<hr/>

```js
<section className='flex justify-center items-center min-h-screen'>
  <div className='flex flex-col items-start space-y-4 p-6 bg-white rounded-lg w-full max-w-4xl'>
    <h3 className='text-lg text-blue-600 font-bold'>EXPERIENCE</h3>
    <div className='flex justify-between w-full h-auto'>
      <p className='text-lg font-semibold'>
        Target
      </p>
      <p className='text-sm text-gray-800 font-bold text-right'>
        SEP 2021 – AUG 2026
      </p>
    </div>
    <div className='flex justify-between w-full'>
      <div className='flex flex-col space-y-2'>
        <p className='text-sm text-gray-600 italic'>
          Guest Advocate, Cart/Store Attendant
        </p>
        <ul className='list-disc list-inside space-y-2 text-gray-600'> 
          <li className='text-sm text-gray-600'>
            Enhanced guest experience by welcoming, thanking, and exceeding service expectations.
          </li>
          <li className='text-sm text-gray-600'>
            Focused on guest interaction and effective resolution of service issues.
          </li>
        </ul>
      </div>
    </div>
  </div>
</section>
```


### Creating the portfolio

Now that you have the education and experience pages done, let's move on to the third section! 

If you are a CS major or intend to work in the computer science field, this will be where you put all of your personal projects.

If you are not, this is a great place to put research, writing samples, etc.

We will build this out step by step during the in-person workshop, but to cut things short here, this is how it should resemble.

```js
{/* PROJECTS */}
<div className='flex flex-col items-start space-y-4 p-6 rounded-lg w-full max-w-6xl'>
<h3 className='text-lg text-blue-600 font-bold'>PROJECTS</h3>
</div> 
<section className='flex justify-center items-center min-h-full'>
  <div className="flex flex-col gap-10 py-10 lg:flex-row lg:flex-wrap">
    <div className="basis-1/3 flex-1 ">
      <h3 className='text-m text-blue-600 font-bold'>Portfolio Website</h3>
      <Image
        className="rounded-lg object-cover"
        layout="responsive"
        alt="project image"
        src={web1}
      />
    </div>
    <div className="basis-1/3 flex-1">
    <Image
        className="rounded-lg object-cover"
        layout="responsive"
        alt="project image"
        src={web2}
      />
    </div>
    <div className="basis-1/3 flex-1">
    <Image
        className="rounded-lg object-cover"
        layout="responsive"
        alt="project image"
        src={web3}
      />
    </div>
    <Image
        className="rounded-lg object-cover"
        layout="responsive"
        alt="project image"
        src={web4}
      />
    <div className="basis-1/3 flex-1">
    <Image
        className="rounded-lg object-cover"
        layout="responsive"
        alt="project image"
        src={web5}
      />
    </div>
    <div className="basis-1/3 flex-1">
    <Image
        className="rounded-lg object-cover"
        layout="responsive"
        alt="project image"
        src={web6}
      />
    </div>
  </div>
</section>
```

<hr />

## Implementing responsive web design 

When creating your portfolio, one thing to keep in mind is making sure that it is responsive to a variety of devices and renders well no matter the window or screen size of the device.

### Responsive padding

   Adjust padding based on screen size to optimize space usage:

   ```jsx
   <main className='bg-white px-4 sm:px-10 md:px-20 lg:px-40'>
   ```

   This provides less padding on mobile devices and gradually increases it for larger screens.

### Responsive typography

   Adjust font sizes for different screen sizes:

   ```jsx
   <h2 className='text-lg sm:text-xl py-2 text-blue-600 font-semibold'>KATHY ROWE</h2>
   <h3 className='text-2xl sm:text-3xl py-2 text-gray-800 font-black'>28th President of William & Mary 👋</h3>
   ```

   This ensures readable text on small screens while allowing for larger, more impactful text on bigger screens.

### Consistent paragraph layout

   Set a maximum width and center the text for a more consistent shape and alignment:

   ```jsx
   <p className='text-sm sm:text-md py-3 sm:py-5 text-gray-800 max-w-lg mx-auto sm:mx-0'>
     Nationally recognized as an innovator in higher education,
     I champion the liberal arts, entrepreneurship and
     strengthening education-workforce pathways.
   </p>
   ```

   The `max-w-lg` class sets a maximum width, while `mx-auto` centers the text on small screens. `sm:mx-0` aligns it to the left on larger screens.

### Responsive images

   Adjust image size based on screen size:

   ```jsx
   <div className='bg-gradient-to-b from-blue-600 rounded-full w-64 h-64 sm:w-72 sm:h-72 md:w-80 md:h-80 lg:w-96 lg:h-96 relative overflow-hidden mb-6 sm:mb-0 flex-shrink-0'>
     <Image src={kathy} alt='profile_pic' layout='fill' objectFit='cover' />
   </div>
   ```

   This progressively increases the image size as the screen gets larger, ensuring it looks good on all devices.

### Responsive layout

   Adjust the layout for different screen sizes:

   ```jsx
   <div className='flex flex-col-reverse sm:flex-row justify-center items-center min-h-[65vh]'>
     <div className='text-center sm:text-left p-4 sm:p-10 w-full sm:w-1/2'>
       {/* Content here */}
     </div>
     {/* Image div here */}
   </div>
   ```

   This stacks the content vertically on small screens and switches to a side-by-side layout on larger screens.

### Responsive icons

   Adjust icon sizes and spacing for different screen sizes:

   ```jsx
   <div className='flex justify-center sm:justify-start py-3'>
     <div className='flex gap-4 sm:gap-6 md:gap-8 lg:gap-10'>
       <a href='https://www.linkedin.com/in/katherine-rowe-2a711545' className='text-2xl sm:text-3xl md:text-4xl lg:text-5xl text-gray-800 hover:text-blue-600 transition-colors'>
         <AiFillLinkedin />
       </a>
       {/* Other icons */}
     </div>
   </div>
   ```

   This adjusts the icon size and spacing between icons based on screen size, while also adding hover effects for better interactivity.

By implementing these responsive design techniques, your portfolio will look great and function well across a wide range of devices, from mobile phones to large desktop screens.

## Adding dark mode

Go back to the top of the `page.tsx` file and add this import statement.

```js
import { useState } from 'react';
```

> `useState` is a React Hook that lets you add a state variable to your component and returns an array with exactly two values:
>
> 1. The current state. During the first render, it will match the initialState you have passed.
> 2. The set function that lets you update the state to a different value and trigger a re-render.
>
> Because `useState` is a Hook, you can only call it at the top level of your component or your own Hooks. You can’t call it inside loops or conditions. If you need to do that, extract a new component and move the state into it. Interested in learning more? Read the React docs here: https://react.dev/reference/react/useState.

Now, go to the top of the `Page` function responsible for rendering your portfolio and initialize a state variable to manage dark mode enabling.

```js
export default function Page() {
  const [darkMode, setDarkMode] = useState(false);
```

Tailwind should already be able to check your system preferences or browser settings to see if you're in dark mode and adapt accordinly, but what we want to be able to toggle between dark and light mode by clicking this button. To do that, you need to modify the `tailwind.config.js` file. 

What adding this line in `module.exports` means is that you now are able to toggle dark mode based off a class and not anything externally. To trigger this, all you need to do is add a class name to the entire web app.

```js
return (
    <div className={darkMode ? 'dark' : ''}>
```

Adding this class will likely trigger an error if you have Next.js 13+ installed. This is because, by default, all components in the App Router are Server Components where these APIs are not available. By defining the "use client" directive in toggle.js, you can tell React to enter the client boundary where these APIs are available.

To fix this, add this line to the very top of your file, even before all the import statements. 

```js
'use client'
```

Read up on the Next.js docs if you're curious about what caused this error:  https://nextjs.org/docs/app/building-your-application/rendering/client-components.

Now, locate the line where the dark mode icon resides and add the following code.

```js
<BsFillMoonStarsFill onClick={() => setDarkMode(!darkMode)} className='cursor-pointer text-2xl'/>
```

This adds an `onClick` event whenever this icon is clicked and sets it to an arrow function that toggles dark mode.

Then, you're going to add the following classes to some of your elements to style this page when it's in dark mode.

```js
<main className='bg-slate-50 px-4 sm:px-10 md:px-20 lg:px-40 dark:bg-gray-900'>
```

```js
<nav className='py-6 sm:py-10 mb-8 sm:mb-12 flex flex-col sm:flex-row justify-between items-center dark:text-white'>
```

```js
<h3 className='text-2xl py-2 text-gray-800 font-black  dark:text-white'>28th President of William & Mary 👋</h3>
<p className='text-md py-3 sm:py-5 text-gray-800 max-w-lg mx-auto sm:mx-0 dark:text-white'>
  Nationally recognized as an innovator in higher education,
  I champion the liberal arts, entrepreneurship and
  strengthening education-workforce pathways.
</p>
```

```js
<div className='text-3xl sm:text-4xl md:text-5xl flex justify-center sm:justify-start gap-8 py-3 text-gray-800 dark:text-white'>
  <a href='https://www.linkedin.com/in/katherine-rowe-2a711545' className='text-2xl sm:text-3xl md:text-4xl lg:text-5xl text-gray-800 hover:text-blue-600 transition-colors dark:text-white'>
    <AiFillLinkedin />
  </a>
  <a href='https://x.com/williamandmary' className='text-2xl sm:text-3xl md:text-4xl lg:text-5xl text-gray-800 hover:text-blue-400 transition-colors dark:text-white'>
    <AiFillTwitterCircle />
  </a>
  <a href='https://www.github.com/gdscwm' className='text-2xl sm:text-3xl md:text-4xl lg:text-5xl text-gray-800 hover:text-gray-600 transition-colors dark:text-white'>
    <AiFillGithub />
  </a>
  <a href='mailto:president@wm.edu' className='text-2xl sm:text-3xl md:text-4xl lg:text-5xl text-gray-800 hover:text-red-500 transition-colors dark:text-white'>
    <AiFillMail />
  </a>
</div>
```

The last two sections feature more extensive modifications, so they are detailed in full below.

```js
{/* EDUCATION */}
<section className='flex justify-center items-center'>
  <div className='flex flex-col items-start space-y-4 p-6 bg-white rounded-lg w-full max-w-4xl dark:bg-gray-800'>
    <h3 className='text-lg text-blue-600 font-bold'>EDUCATION</h3>
    <div className='flex justify-between w-full h-auto'>
      <p className='text-lg font-semibold dark:text-white'>
        College of William and Mary
      </p>
      <p className='text-sm text-gray-800 font-bold text-right dark:text-white'>
        MAY 2026
      </p>
    </div>
    <div className='flex flex-col space-y-2'>
      <p className='text-m text-gray-600 italic dark:text-white'>
        Bachelor's of Science in Computer Science
      </p>
      <p className='text-sm text-gray-600 dark:text-white'>
        Coursework: Computational Problem Solving, Calculus II
      </p>
    </div>
    <div className='flex justify-between w-full h-auto mt-4'>
      <p className='text-lg font-semibold dark:text-white'>
        Random High School
      </p>
      <p className='text-sm text-gray-800 font-bold text-right dark:text-white'>
        MAY 2022
      </p>
    </div>
    <div className='flex justify-between w-full'>
      <div className='flex flex-col space-y-2'>
        <p className='text-m text-gray-600 italic dark:text-white'>
          High School Diploma
        </p>
        <p className='text-sm text-gray-600 dark:text-white'>
          Coursework: AP Computer Science A, CS Programming, Web Page Development, Calculus I
        </p>
      </div>
    </div>
  </div>
</section>
```

```js
{/* EXPERIENCE */}
<section className='flex justify-center items-center min-h-screen'>
  <div className='flex flex-col items-start space-y-4 p-6 bg-white rounded-lg w-full max-w-4xl dark:bg-gray-800'>
    <h3 className='text-lg text-blue-600 font-bold'>EXPERIENCE</h3>
    <div className='flex justify-between w-full h-auto'>
      <p className='text-lg font-semibold dark:text-white'>
        Target
      </p>
      <p className='text-sm text-gray-800 font-bold text-right dark:text-white'>
        SEP 2021 – AUG 2026
      </p>
    </div>
    <div className='flex justify-between w-full'>
      <div className='flex flex-col space-y-2'>
        <p className='text-sm text-gray-600 italic dark:text-white'>
          Guest Advocate, Cart/Store Attendant
        </p>
        <ul className='list-disc list-inside space-y-2 text-gray-600'> 
          <li className='text-sm text-gray-600 dark:text-white'>
            Enhanced guest experience by welcoming, thanking, and exceeding service expectations.
          </li>
          <li className='text-sm text-gray-600 dark:text-white'>
            Focused on guest interaction and effective resolution of service issues.
          </li>
        </ul>
      </div>
    </div>
  </div>
</section>
```

<hr/>

## Credit

This workshop was inspired by the following resources:
- developedbyed's [React Portfolio Website With Tailwind Tutorial](https://www.youtube.com/watch?v=k-Pi5ZMxHWY) on YouTube.
<!-- compiletab's [React Portfolio Website With Tailwind Tutorial](https://www.youtube.com/watch?v=_63mEm3AMSY&t=1772s) on YouTube. -->
- [Stefan Topalovic's portfolio](https://www.stefantopalovic.com/).

<hr/>

## More information

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
