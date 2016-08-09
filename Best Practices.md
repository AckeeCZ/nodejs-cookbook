# Best practices

## Table of Contents

## ESLint

### About

ESLint is used for static control of quality of your code and for coding standards.

### How to use

Each project has stored in package.json script for running the eslint with lint for linux/mac and lint-win for windows.

### Why do we use it

It is very easy to set up - either on your local machine either in continues integration process.

Also having same standards is always good and prevents a lot of potentional bugs.

### What rules do we use

We decided that we should look to succesfull companies to see, how they roling. We liked a lot an [airbnb javascript guide][1], therefore that was the starting point. We managed to go through each rule and decide if we want to follow it. Some points where changed (i.e. changed from error to warning), but most of it stayed same as theirs.

### How does it help us

For example the "Additional trailing comma" helped us a lot with merging. At first it did not look good. Why adding meaningless comma at the end of objects like this?

```javascript
    const myObject = {
        something: true,
        something2: true,
    }
```

Well when you are merging branches in GIT, the line can disappear or be added. With code like this :

```javascript
    const myObject = {
        something: true,
        something2: true
    }
```

When new line is added, the object becomes uncompilable

```javascript
    const myObject = {
        something: true,
        something2: true
        something3: true
    }
```

When everyone have comma at the end of line, you are safe to do almost anything and you dont have to be scared for "what if merge of these branches make my code uncompilable?"

[1]:	https://github.com/airbnb/javascript