# le-gulp-sass
Learn Gulp &amp;&amp; Sass engine from scratch

***

## What is Gulp?
Gulp is a tool that helps you out with several tasks when it comes to web development. It's often used to do front end tasks like:

* Spinning up a web server
* Reloading the browser automatically whenever a file is saved
* Using preprocessors like Sass or LESS
* Optimizing assets like CSS, JavaScript, and images

This is not a comprehensive list of things Gulp can do. If you're crazy enough, you can even build a static site generator with Gulp (I've done it!). So yes, Gulp is extremely powerful, but you'll have to learn how to use Gulp if you want to create your own customized build processes.

So that's what this article is for. It helps you get so good with the basics of Gulp that you can begin exploring everything else for yourself.

Before we dive into working with Gulp, let's talk about why you may want to use Gulp as opposed to other similar tools.

## Why Gulp?
Tools like Gulp are often referred to as "build tools" because they are tools for running the tasks for building a website. The two most popular build tools out there right now are Gulp and Grunt. 
The main difference is how you configure a workflow with them. Gulp configurations tend to be much shorter and simpler when compared with Grunt. Gulp also tends to run faster.
Let's now move on and find out how to setup a workflow with Gulp.

## What we're setting up

### Installing Gulp
You need to have Node.js (Node) installed onto your computer before you can install Gulp.

If you do not have Node installed already, you can get it by downloading the package installer from [Node's website](https://nodejs.org/en/).

When you're done with installing Node, you can install Gulp by using the following command in the command line:
```javascript
  npm install gulp -g
```
                
The `npm install` command we've used here is a command that uses Node Package Manager (npm) to install Gulp onto your computer.

The `-g` flag in this command tells npm to install Gulp globally onto your computer, which allows you to use the gulp command anywhere on your system.

### Creating a Gulp Project
First, we'll create a folder called **`Cyas`** to server as our project root as we move through this tutorial. Run the npm init command from inside that directory:
```javascript
  npm init
```
After run `npm init` we have a `package.json` file:

![package.json file](/images/package.png)

Once the package.json file is created, we can install Gulp into the project by using the following command:
```javascript
  npm install gulp --save-dev
```

![package.json file](/images/package.png)

### Determining Folder Structure
Gulp is flexible enough to work with any folder structure. You'll just have to understand the inner workings before tweaking it for your project.

For this article, we will use the structure of a generic web-app:

![package.json file](/images/structure.png)

In this structure, we'll use the app folder for development purposes, while the dist (as in "distribution") folder is used to contain optimized files for the production site.

Since app is used for development purposes, all our code will be placed in app.

We'll have to keep this folder structure in mind when we work on our Gulp configurations. Now, let's begin by creating your first Gulp task in gulpfile.js, which stores all Gulp configurations.

### Writing Your First Gulp Task
The first step to using Gulp is to `require` it in the gulpfile.
```javascript
  var gulp = require('gulp');
```

The require statement tells Node to look into the `node_modules` folder for a package named `'gulp'`. Once the package is found, we assign its contents to the variable `gulp`.

We can now begin to write a gulp task with this `gulp` variable. The basic syntax of a gulp task is:
```javascript
  gulp.task('task-name', function() {
    // Stuff here
  });
```

`'task-name'` refers to the name of the task, which would be used whenever you want to run a task in Gulp. You can also run the same task in the command line by writing gulp `'task-name'`.

To test it out, let's create a hello task that says `Hello Sflircs!`.
```javascript
  gulp.task('hello', function() {
    console.log('Hello Sflircs');
  });
```

We can run this task with `gulp hello` in the command line.
```javascript
  gulp hello
```

Gulp tasks are usually a bit more complex than this. It usually contains two additional Gulp methods, plus a variety of Gulp plugins.

Here's what a real task may look like:
```javascript
  gulp.task('task-name', function () {
    return gulp.src('source-files') // Get source files with gulp.src
      .pipe(aGulpPlugin()) // Sends it through a gulp plugin
      .pipe(gulp.dest('destination')) // Outputs the file in the destination folder
  })
```

As you can see, a real task takes in two additional gulp methods — `gulp.src` and `gulp.dest`.

`gulp.src` tells the Gulp task what files to use for the task, while `gulp.dest` tells Gulp where to output the files once the task is completed.

Let's try building a real task where we compile Sass files into CSS files.

### Preprocessing with Gulp
We can compile Sass to CSS in Gulp with the help of a plugin called `gulp-sass`. You can install `gulp-sass` into your project by using the `npm install` command like we did for `gulp`.

We'd also want to use the `--save-dev` flag to ensure that `gulp-sass` gets added to `devDependencies` in **`package.json`**.
```javascript
  npm install gulp-sass --save-dev
```

We have to require `gulp-sass` from the `node_modules` folder just like we did with `gulp` before we can use the plugin.
```javascript
  var gulp = require('gulp');
  // Requires the gulp-sass plugin
  var sass = require('gulp-sass');
```

The task is meant to compile Sass into CSS, let's name it sass.
```javascript
  gulp.task('sass', function(){
    return gulp.src('source-files')
      .pipe(sass()) // Using gulp-sass
      .pipe(gulp.dest('destination'))
  });
```

Refs: https://css-tricks.com/gulp-for-beginners/
