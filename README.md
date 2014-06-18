Drupal Grunt Build and Testing Tools
===

Requirements
---

* Node.js
* Grunt CLI


Getting started
---

Including in an existing project:

1. Copy Gruntconfig.json and Gruntfile.js from this project's example directory to your project. Add the grunt and drupal-grunt-starter dependency to your package.json or copy package.json as well.

1. Run "npm install" to install dependencies.

Setting up a new project:

1. In an empty directory, run: npm install --save-dev grunt git+ssh://git@bitbucket.org/phase2tech/drupal-grunt-starter.git

1. Copy the contents of node_modules/drupal-grunt-starter/example to the project directory.

Supporting the validate task:

1. Create or modify your project's composer.json file to include `squizlabs/php_codesniffer` and `drupal/coder` as demonstrated in example/composer.json

Configuration
---

1. Update Gruntconfig.json as needed to specify a custom source or build path or to enable Compass SASS to CSS compilation for custom themes.

1. Update Gruntconfig.json as needed to specify the path to the PHPCS binary and the Drupal Coder module PHPCS standard.


Extending
---

1. Update Gruntfile.js as needed to add build steps or other project-specific actions.

