## Upgrade your Tailwind CSS project to version 3.0

Christmas came early for TailwindCSS lovers as Tailwind Labs released the third version of their earth-shattering CSS framework on December 9th.

This upgrade comes with loads and loads of new features and upgrades that are aimed at making the developer's life a lot easier and helping to speed up the development process.

The topmost features include the Just-in-time all the time, which comes straight out the box now, extended color palettes, colored box-shadows (Lord knows how much I've wanted those... ), colored links, etc. 


> You can check out the [official documentation](https://tailwindcss.com/blog/tailwindcss-v3)  to see the full list of features.


### Assumptions made in this post; 


- That you are familiar with Tailwind, currently using previous versions, and are looking to upgrade to v3... I mean that's why we're here eh?

- You have your code hosted in remote repos on Github, Gitlab, or Bitbucket. If you're not familiar with Git version control, you can check out some quick tutorials on youtube as there are hundreds of those.

- That some of the projects that need upgrading may be live. *Don't worry, we won't alter anything in production.*


### Upgrading to v3


> It's easier than it sounds... trust me, but before we begin, I'd strongly advise creating a new branch of your project where you will carry out the upgrade... in other to avoid tears and heartbreaking stories. You can merge later when you're done and finally push to production. 

 We would be upgrading via **Tailwind CLI** and **PostCSS** depending on your preference.

### Upgrading via Tailwind CLI

This is the simplest way to be up and running in no time and mostly when you're not using any build tools.




#### Install Tailwind

While at the root of your project, open up the terminal and type this command

```
npm install -D tailwindcss
``` 
This installs v3 of Tailwind in your project

Seeing as we already have the `package.json` and `tailwind.config.js` files on our project, we don't need to create new ones.

In your `package.json` file, you'll see that a new object has been added like this 

```
"devDependencies": {
    "tailwindcss": "^3.0.7"
  }
``` 
As of the time of writing this, the current version was 3.0.7.

#### Configure your template paths

In v3, purgeCss is no more supported so you have to replace the `purge` array in the `tailwind.config.js` file with `content` and add the paths to all your template files where the utility classes are mentioned... this is so that Tailwind knows the files to scan and build only the required classes to your stylesheet.


```
module.exports = {
  content: ["./dist/**/*.html",
  "./dist/**/*.js"],
  theme: {
    extend: {},
  },
  plugins: [],
}
``` 
You can remove the `dark mode` configuration and `variants` from the config file as well since they're no more supported.

#### Building your CSS

If you were using a build script in your previous setup, you can leave it that way so far as you didn't change the file paths for your input and output stylesheets.

If you weren't, you can add a build script to the `scripts` in your `package.json` 


```
"scripts": {
    "build": "npx tailwindcss -i ./src/input.css -o ./dist/output.css --watch"
  },
``` 
You can now build your CSS with this


```
npm run build
``` 
Alternatively, you can ditch the build script and just run this directly on your terminal


```
npx tailwindcss -i ./src/input.css -o ./dist/output.css --watch

``` 

And just like that, your CSS file would have been replaced with the new Tailwind version and a greatly reduced file size all thanks to the Just-in-time all the time feature.

### Upgrading via PostCSS

This is particularly useful only when you're using other build tools  like webpack in your project

#### Install Tailwind

Please note that v3 does not support PostCSS 7 and you'd be required to upgrade to PostCSS 8.

This will be achieved by installing the latest versions of tailwind, postcss, and autoprefixer. 


```
npm install -D tailwindcss postcss-cli autoprefixer

``` 
Create your tailwind and postcss config files via npx, you can skip this if you already have these files in your project.


```
npx tailwindcss init -p
``` 
This creates the `tailwind.config.js` and `postcss.config.js` files in your root folder.

Once again, you can remove the `dark mode` configuration and `variants` from the config file as well since they're no more supported.

From here, it's the same process with the Tailwind CLI method

#### Configure your template paths

```
module.exports = {
  content: ["./dist/**/*.html",
  "./dist/**/*.js"],
  theme: {
    extend: {},
  },
  plugins: [],
}
``` 

> Remember to replace `purge` with `content`



#### Building your CSS



```
"scripts": {
    "build": "postcss ./src/input.css -o ./dist/output.css --watch"
  },

``` 

In case this doesn't work as may be the case for some windows users, use this instead

```
"scripts": {
    "build": "TAILWIND_MODE=WATCH postcss ./src/input.css -o ./dist/output.css --watch"
  },

``` 
At this point, your stylesheet should have been built with the new version and you're good to go.


> The next thing to do is head on to the [documentation](https://tailwindcss.com/) to apply any breaking changes in your code.

Thank you for sticking around to the end, and please leave a comment if you're stuck at any point.






