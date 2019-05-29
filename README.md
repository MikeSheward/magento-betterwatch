# magento-betterwatch
### A better watcher for Magento 2, using BrowserSync.
This can be used instead of LiveReload as a way to show your Less/CSS + JS changes directly in the browser without the need to refresh the page and lose the current page state. It's super easy to add to your Magento 2 project too. You can implement this with an existing Magento 2 project or a brand new one.

## Installation
You can get using this with just a few minor steps...

Create the following Grunt config files inside your Magento project.
#### /dev/tools/grunt/configs/browserSync.js
```
'use strict';

module.exports = {
    "files": [ "pub/static/frontend/**/*.css", "pub/static/frontend/**/*.js" ],
    "options": {
      "proxy": process.env.BW_PROXY
    },
};
```

#### /dev/tools/grunt/configs/concurrent.js
```
'use strict';

module.exports = {
    frontend: ['browserSync', 'watch'],
    options: {
        logConcurrentOutput: true
    }
};
```

Create the following Grunt task file inside your Magento project.
#### /dev/tools/grunt/tasks/betterwatch.js
```
module.exports = function (grunt) {
    'use strict';

    grunt.registerTask('betterwatch', function() {

        grunt.log.subhead('Initialising Magento 2 Better Watcher by Develo Design');

        grunt.task.run( 'concurrent:frontend' );

    });

};
```

Add the following snippets to your package.json file inside your Magento project. Be sure to add both "grunt-browser-sync" and "grunt-concurrent" dependencies to the devDependencies inside your package.json file. Also add the below scripts section to file also. 
###### Note: Be sure to replace "magentoproject.local" inside the betterwatch script in your package.json file to the domain that you are using for your magento project.
#### /package.json
```
{
    ...
    "devDependencies": {
        ...
        "grunt-browser-sync": "^2.2.0",
        "grunt-concurrent": "^2.3.1"
    },
    "scripts": {
        "betterwatch": "BW_PROXY=magentoproject.local grunt betterwatch"
    }
}
```

## Usage
Run it using
```
npm run betterwatch
```

## Tada
Thats it! It will run the magento 2 default watcher and the BrowserSync watcher simultaniously, allowing you to edit your Magento 2 theme Less files and allow the changes to be displayed live in the browser, automatically injected with zero hassle. It will still output your usual Magento Less watcher errors in the console alongside any browsersync running errors.

