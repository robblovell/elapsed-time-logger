# Elapsed time logger
Similiar to console.time() & console.timeEnd() but returns formatted elapsed time `custom label: 4 hours 10 minutes 23.5 seconds` or if less then a second: `540ms`
Works in NodeJS and in browser.

![CircleCI](https://img.shields.io/circleci/build/github/vltansky/elapsed-time-logger)
[![Coverage Status][coveralls-image]][coveralls-url]
[![npm version](https://img.shields.io/npm/v/elapsed-time-logger)](https://www.npmjs.com/package/elapsed-time-logger)
![David](https://img.shields.io/david/vltansky/elapsed-time-logger)
![npm bundle size](https://img.shields.io/bundlephobia/min/elapsed-time-logger)
![NPM](https://img.shields.io/npm/l/elapsed-time-logger)
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fvltansky%2Felapsed-time-logger.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Fvltansky%2Felapsed-time-logger?ref=badge_shield)


[coveralls-image]: https://img.shields.io/coveralls/github/vltansky/elapsed-time-logger
[coveralls-url]: https://coveralls.io/github/vltansky/elapsed-time-logger

package depends on [Browser-hrtime](https://github.com/vltansky/browser-hrtime)
# Install
`$ npm i elapsed-time-logger`
# Usage

## NodeJS
```js
const elapsed = require("elapsed-time-logger");
// chalk is't required, added as example to show that you can use colors in output
const chalk = require('chalk');
 
// elapsed is similliar to console.time() & console.timeEnd() 
elapsed.start('label');
elapsed.start('label_id');
setTimeout(()=>{
    elapsed.end('label');//output: label 801ms
    elapsed.end('label_id', 'Text that goes here will override label on output');
    // output: Text that goes here will override label on output 801ms
}, 800);
// if paramter label is not provided, start() will return an instance 
const elapsedTimer = elapsed.start();
const elapsedTimer2 = elapsed.start();
setTimeout(()=>{
    elapsedTimer2.end(chalk.green('you can use colors here, try chalk or colors packages:'));
    // output: you can use colors here, try chalk or colors packages: 806ms
    const time = elapsedTimer.get();//return 806ms
    console.log(time);
    elapsedTimer.end('finished:');// output: finished: 806ms
}, 800);
```
<img src="node.png">

## ESM (Browser e.g Angular, react, etc.)
```js
import elapsed from 'elapsed-time-logger';
elapsed.start('test2');
setTimeout(()=>{
    elapsed.end('test2');
}, 1300);


elapsed.start('test');
setTimeout(()=>{
    elapsed.end('test');
}, 1300);

elapsed.start('testoverride');
setTimeout(()=>{
    elapsed.end('testoverride', 'override label');
}, 100);


elapsed.start('vlad');
setTimeout(()=>{
    const test = elapsed.get('vlad');
    console.log(test);
}, 1200);

// ElapsedLogger is similliar to console.time() & console.timeEnd() 
elapsed.start('label');
elapsed.start('timer label');
setTimeout(()=>{
    elapsed.end('label');
    elapsed.end('timer label');
}, 800);


// or use ElapsedLogger as an instance (recommended)
const elapsedTimer = elapsed.start();
// const elapsedTimer2 = elapsed.start();
console.log('smth');
setTimeout(()=>{
    const t = elapsedTimer.get();
    console.log(t);
    // elapsedTimer2.end(chalk.green('you can use colors here, try chalk or colors packages:'));
    elapsedTimer.end('finished:');
}, 800);
```
<img src="browser.png">

## UMD
```html
<!DOCTYPE html>
<html>

<head>
    <script crossorigin src="https://unpkg.com/elapsed-time-logger/lib/umd/index.js"></script>
    <script>
    var elapsed = Elapsed_logger;
    elapsed.start('test2');
    setTimeout(()=>{
        elapsed.end('test2');
    }, 1300);


    elapsed.start('test');
    setTimeout(()=>{
        elapsed.end('test');
    }, 1300);

    elapsed.start('testoverride');
    setTimeout(()=>{
        elapsed.end('testoverride', 'override label');
    }, 100);


    elapsed.start('vlad');
    setTimeout(()=>{
        const test = elapsed.get('vlad');
        console.log(test);
    }, 1200);

    // ElapsedLogger is similliar to console.time() & console.timeEnd() 
    elapsed.start('label');
    elapsed.start('timer label');
    setTimeout(()=>{
        elapsed.end('label');
        elapsed.end('timer label');
    }, 800);


    // or use ElapsedLogger as an instance (recommended)
    const elapsedTimer = elapsed.start();
    // const elapsedTimer2 = elapsed.start();
    console.log('smth');
    setTimeout(()=>{
        const t = elapsedTimer.get();
        console.log(t);
        // elapsedTimer2.end(chalk.green('you can use colors here, try chalk or colors packages:'));
        elapsedTimer.end('finished:');
    }, 800);


    </script>
</head>

<body>
</body>

</html>
```

## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fvltansky%2Felapsed-time-logger.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Fvltansky%2Felapsed-time-logger?ref=badge_large)