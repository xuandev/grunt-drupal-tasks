# Drupal Grunt Build and Testing Tools

Code Status (master branch):
<a href="https://travis-ci.org/phase2/grunt-drupal-tasks"><img src="https://travis-ci.org/phase2/grunt-drupal-tasks.svg?branch=master"></a>

## Requirements

* Node.js

## Features

This project is built on the tools of the grunt community to provide scripted
automation of a number of PHP & Drupal tasks from wrangling the UI all the way
down to build & deployment processes. Here are just a few examples of what it
provides:

* PHP code quality checks
* Compass compilation
* Drush make-based build workflow
* Deployment packaging
* Behat testing
* Jenkins support
* Extensibility: Add or override anything with your own plugins or configuration.

We are continuously working to improve this toolchain, adding functionality that
we see as common to our _continuous integration_ and everyday development practices.

## Getting started

If you would like to use grunt-drupal-tasks, be prepared to use it as a
dependency and light framework for your project's use of grunt.

### Add to an existing project

1. Copy Gruntconfig.json, Gruntfile.js, and composer.json from this project's
example directory to your project. Add the grunt and grunt-drupal-tasks
dependency to your package.json or copy package.json as well.

2. Run "npm install" to install dependencies.

### Set up a new project

1. In an empty directory, run:
   `npm install --save-dev grunt git+https://github.com/phase2/grunt-drupal-tasks.git`
2. Copy the contents of node_modules/grunt-drupal-tasks/example to the project
   directory.

## Task-specific dependencies

### Supporting the validate and analyze tasks

* Create or modify your project's composer.json file to include
`squizlabs/php_codesniffer`, `grunt-phpmd`, and `drupal/coder` as demonstrated
in example/composer.json

## Configuration

1. Update Gruntconfig.json as needed to specify a custom source or build path
   or to enable Compass SASS to CSS compilation for custom themes.
2. Update Gruntconfig.json as needed to specify the path to the PHPCS binary
   and the Drupal Coder module PHPCS standard.

## Customizing

You may add any project-specific directives you want to your Gruntfile.js.

### Changing the Default Build Process

There are two ways to change the default build process (which is run when simply
typing `grunt` into the command-line.)

1. Replicate the definition of the default task you can see in this
   grunt-drupal-tasks' Gruntfile.js. This will completely replace what currently
   exists.
2. Use a slick workaround that allows you to keep the default task as it's been
   defined, but append or prepend your own operations. See below for a simple
   example.

```js
grunt.task.rename('default', 'default-original');
grunt.registerTask('default', ['shell:custom', 'default-original']);
```

### Leveraging Bash Scripts

If you have an existing project or a kit of useful project utilities, you may
have some Bash scripts laying around that you want to keep. You can fold them
into the grunt tools and worry about reimplementing them later using something
like the simple wrapper script based on
[grunt-shell](https://github.com/sindresorhus/grunt-shell) displayed below.

```js
module.exports = function(grunt) {
 
/**
 * Define "bin" wrapper tasks.
 */
var files = grunt.file.expand("bin/*.sh");
if (files) {
  for (var f in files) {
    var name = files[f].split('/').pop().split('.').shift();
      grunt.config(['shell', name], {
        command: 'bash ' + files[f]
      });
      grunt.registerTask(name, ['shell:' + name]);
    }
  }
};
```
This particular snippet requires your bash scripts end in `.sh` and be located
in the directory `root:bin/`.
