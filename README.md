## Introduction
Javascript Unit Testing using karma together with Mocha, Chai and requirejs. You can just test the code alone using Mocha, just
imagine you've a lot of test suite, it's best if we can watch the changes, generate the report, etc by using Karma(not Wings hukum karma okey)!

## Requirements
 - Karma(Test Runner)
 - Mocha(Test Framework)
 - Chai
 - RequireJs(Module dependencies)
 - npm
 
 ## Steps
 0) create project directory with any name <my-project>
 1) Create package.json file `npm init`
 2) Installing karma, mocha, requirejs, chai and all plugins related to karma
 
    a) Install karma and karma plugins
      ```
      npm i --save-dev karma
      npm i --save-dev karma-mocha
      npm i --save-dev karma-chai
      npm i --save-dev karma-requirejs
      ```
      
    b) Install mocha, requirejs and chai
      ```
      npm i --save-dev mocha
      npm i --save-dev chai
      npm i --save-dev requirejs
      ```
      
    c) Install launcher
      ```
      npm i karma-chrome-launcher --save-dev
      npm i karma-firefox-launcher --save-dev // optional
      npm i karma-opera-launcher --save-dev // optional
      npm i karma-safari-launcher --save-dev // optional
      npm i karma-phantomjs-launcher --save-dev // optional
      npm i phantomjs --save-dev // optional
      ```
      
    d) Install karma-cli, for enabling karma command as a global `npm i -g karma-cli`
 
 3) Create `karma.conf.js`file using following command `karma init` --> this command will create karma.conf.js. Or copy 
 from the code below and paste into `karma.conf.js` :
 
 ```javascript
 // Karma configuration
 // Generated on Thu Oct 19 2017 15:23:52 GMT+0800 (+08)

module.exports = function(config) {
  config.set({

    // base path that will be used to resolve all patterns (eg. files, exclude)
    basePath: '',


    // frameworks to use
    // available frameworks: https://npmjs.org/browse/keyword/karma-adapter
    frameworks: ['mocha', 'requirejs', 'chai'],

    // set plugins that we need to use with karma during test execution
    plugins : [
      'karma-phantomjs-launcher',
      'karma-mocha',
      'karma-requirejs',
      'karma-chai',
      'karma-chrome-launcher'   
    ],

    // list of files / patterns to load in the browser
    files: [
        {pattern: './unit-tests/**/*.js', included: true}, // where out test suite located
        {pattern: './unit-tests/main.js', included: true} // required all test suite and include into DOM
    ],

    // list of files to exclude
    exclude: [
        './app/private/header/failure.js'
    ],
    
    reporters: ['progress'],


    // web server port
    port: 9876,


    // enable / disable colors in the output (reporters and logs)
    colors: true,


    // level of logging
    // possible values: config.LOG_DISABLE || config.LOG_ERROR || config.LOG_WARN || config.LOG_INFO || config.LOG_DEBUG
    logLevel: config.LOG_INFO,


    // enable / disable watching file and executing tests whenever any file changes
    autoWatch: true,


    // start these browsers
    // available browser launchers: https://npmjs.org/browse/keyword/karma-launcher
    browsers: ['Chrome', 'PhantomJS'],


    // Continuous Integration mode
    // if true, Karma captures browsers, runs the tests and exits
    singleRun: false,

    // Concurrency level
    // how many browser should be started simultaneous
    concurrency: Infinity
  })
}
```

4) Create a folder at the root project name `unit-tests` and create file `main.js` :

```javascript

var tests = [];
// get all test suites that suffix with `_test.js`
for (var file in window.__karma__.files) {
    if (/\_test\.js$/.test(file)) { tests.push(file); }
}
// require above test suite automatically using requirejs
// and finally run mocha programmatically
requirejs.config({
    baseUrl: '/base/app/',
    deps: tests,
    callback: mocha.run
});
```

5) Create simple test suite inside `unit-tests` folder with the name ending with `_test.js`, `eg:my_test.js`:

```javascript
// here we can use chai.expect, chai.should() or chai.assert
var assert = chai.assert;

describe("Init test", function(){
   describe("Equal", function(){
     it("should match count", function(){
     	var a = 1;
       assert.equal(-1, [1,2,3].indexOf(a));
     });
   });
});

```

6) Run test using this command `karma start` or `karma start karma.conf.js`, you can see the results of test inside console 
or at browser's console

7) Have fun.
      
      
