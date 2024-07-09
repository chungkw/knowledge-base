# Handling Command Arguments in NodeJS

#### 30 June 2024

It is common to have a program to have inputs which are used to inform the program or determine its outcome. It is useful during development, allowing the developer to try different configurations and work with different systems, such as:

- Using a local development database or an online one (good for testing cloud deployment)
- Whether to reset and seed the development database or not on startup (good for testing and presentation of prototype)
- Specify an input and output file for the program to process and write to disk (common use case for processing of information)

Yargs is the library to use to handle these scenarios. It is easy to use and configure. It also consists of a useful function that helps clean up the arguments NodeJS provides, such as the command itself used to call NodeJS.

```js
const yargs = require('yargs/yargs');
const { hideBin } = require('yargs/helpers');

const argv = yargs(hideBin(process.argv))
    .alias("m", ["month"])
    .alias("h", ["holidays"])
    .alias("i", ["input"])
    .alias("o", ["output"])
    .parse();
```

The most basic use of Yargs is to simply name the program’s arguments, giving it shorthands and other aliases.

However, you can also better define an argument’s type and further process  and manipulate the inputs into something more useful for the program.

You can set an argument’s type as a string or number, so Yargs can do the typecasting and checking. You can also build arguments as an array of a type.

```js
const argv = yargs(hideBin(process.argv))
    .alias("m", ["month"]).number("month")
    .alias("h", ["holidays"]).number("holidays").array("holidays")
```

(It’s called a builder pattern!)

Number-like entries may be automatically casted as a number, but this can be avoided.

```js
const argv = yargs(hideBin(process.argv))
    .alias("h", ["holidays"]).string("month")
```

It is also possible to manipulate, or coerce, the data as well.

```js
const argv = yargs(hideBin(process.argv))
    .alias("i", ["input"]).string("input")
    .coerce("input", (filename) => path.resolve(__dirname + "/" + filename))
```

In this example, the input argument is a file’s name in the same directory as the program, but resolved to the absolute path on the disk, instead of using a relative path.
