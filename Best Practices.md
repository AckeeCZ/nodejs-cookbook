# Best practices

## Postman

One of the best software ever developed. It makes accessing, sharing and testing of your REST API as easy as possible! We have described some high-level usage [here][4]. If you have not met postman yet, we recommend you to [try it][5]

## ESLint

![Image][image-1]

### About

ESLint is used for static analysis of your code and for coding standards.

### How to use

We have predefined scripts in each project for running the eslint with all required parameters and rules. 

### Why do we use it

It is very easy to set up - either on your local machine or in continous integration process.

Having same standards for all developers in team is always good!

### What rules do we use

We have decided that we should look to succesfull companies.. We enjoyed a lot an [airbnb javascript guide][1], therefore that was the starting point. We managed to go through each rule and decide if we want to follow it. Some points where changed (i.e. changed from error to warning), but we have adapted most of it .

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

Image now that __User A__ add _something3_ and deletes _something2_, __User B__ add _something4_ and also deletes _something2_, therefore it looks as following :

__User A__
```javascript
    const myObject = {
        something: true,
        something3: true
    }
```

__User B__
```javascript
    const myObject = {
        something: true,
        something4: true
    }
```

Guess what happens, when they merge branches together (or to some public i.e. development branch) :

```javascript
    const myObject = {
        something: true,
        something3: true
        something4: true
    }
```

Yes, you end up with code, that crashes as soon as it tries to load file with this object.

When everyone have comma at the end of line, you are safe to do almost anything and you dont have to be scared for "what if merge of these branches make my code uncompilable?"

## Tests

### About

If you read this cookbook, you probably know what automated tests are. We also use it a lot! We even control the  sufficient code coverage. If you write too much code without tests, it can be even reason to not accept your commit into development and/or production branch!

And worst of all, our continues integration system (jenkins) will mark your commit with __this evil picture__: ![Image][image-2]

### Why we use it

Writing tests in beggining of project seems like wasting time. You spend time with writing tests, while it almost never find any additional error. However as project continues, the complexity rises with incoming change-requests from customers (or mobile app/frontend developers, but you know, you are writing the server, you are the master, they have to obey your API #ServerMasterRace).

Bigger the code and complexity, bigger the chance you create bug while fixing another. Everyone at least once said : this new code should _never ever_ affect existing code but it actually __does__ (yes, life is cruel), good written tests are here for you to warn you.

### What tests do we use

In most of our node.js applications, we are focusing on integeration tests that are sending requests to our server. However for some more complex components, we do use _classic_ unit tests.

### Technologies

The [Mocha][2] with [Chai][3] are well supported and popular testing frameworks, therefore we decided to utry them and they serve its purpose.

### Code coverage

As mentioned in _about_ section, we do use code coverage tools, which tells you how good you are covering code with your tests. You can even see in browser all info you need, even marking the lines which was tested and lines which was not (or which branch was executed).

## Npm install

If you are running Node applications, you probably know npm install, which installs all required modules.

### Caret ranges

As recommended by npm cli itself when installing with --save parameter, we use caret ranges, which starst with __^__, i.e. __^1.3.5__. By far we did not have trouble with this approach, as authors of modules are very responsible in making new versions. Using caret ranges can install different version than exactly specified, but it should be always non-breaking change, only bug-fixing or presenting new features.

### Dont send node_modules

The node_modules directory is something that should be present only on runnable environment and you do not want to share it anywhere. Therefore we never send it to our GIT repository or to any other deployment system. Who wants to run our project, he has to run npm install itselft. Also many modules are compiled, therefore they are OS specific after installation.

## Bower

Similar to npm install, the bower allowing installing frontend javascripts and/or css. It also makes easier to distribute application with the right versions without the need of manually checking if i.e. all files have _this_ particular version. Also there is no need to send bower files to GIT or any other system - when needed, it is installed by bower install.

## Promises
_NO MORE CALLBACKS_! Yay!

![Image][image-3]

With ES6 comes the Promises (well they came already before that, but after this, they were finally standartized and included inside Node internal packages). And they are GREAT! Not only for avoiding callback hell, it allows you to take many promises at once and works with them as you need. Also throwing and catching error is really improved as one error catch can satisfy any number of chained promises! (if you used callbacks back then, they always have to start with _if (err) { ... }_

## Social Networks
Almost every popular app has possibility to login/register through the social network. Our apps (yea, extremely popular with fantastic design and no errors at all) are not exception. It is great option we can offer our customers, therefore we do it (almost) anywhere!

We can also recommend it as it is not difficult to implement. Also security is not the issue (facebook/google is handling validity and security of access tokens itself, you just accept their services).

## Version Control
### TODO - take Version Control from iOS cookbook

We use git and gitlab we follow [feature branch workflow][4] for development with merge requests. We have `master` branch where lays production code. in `development` branch we keep *current* development version of the app. 

### Branching 
For every fix or feature you have to create separate branch. When you are done. You create merge request.

### Naming
Name branches with meaningful names which describes what you are trying to do there. When more developers are on the project prefix the name with your initials i.e `dv/fix-login-action`

### Merge Requests 
On every project we do merge requests. If there are 2 developers on project they do cross merge requests. If there is less or more developers you can do round robin assignment within a team. Everyone creates MR even senior developer can assign MR to junior on his project. Why? [here is the explanation]()

- Always choose destination branch the one from which you originally branched.‼️
- Only `development`branch could be merged into `master` 💀 

### Code review
Codereview is done in gitlab. There are 4 levels of reviewer's anger:

| emoji | shortcut          | meaning                                                                                      | merged |   |
|--------|-------------------|----------------------------------------------------------------------------------------------|--------|---|
| ❔      | :grey_question:   | I'm probably just bored and want to talk :)                                                 | YES    |   |
| ❕      | :grey_exclamation | I will merge this but you should either not do this again or defend it here in the comments. | YES    |   |
| ❗      | :exclamation:     | Won't be merged, unless it's a question and you reply that there's no problem.              | MAYBE     |   |
| 💩      | :shit:            | Won't be merged. Also, you should walk through sewers for a month. _(Rarely Used)_           | NO     |   |


Other emojis like ➕ are also used, but we dont need a convention for every emoji out there. ❤ 

[1]:	https://github.com/airbnb/javascript
[2]:    https://mochajs.org/
[3]:    http://chaijs.com/
[4]:	https://github.com/AckeeCZ/nodejs-cookbook/blob/master/Postman%20Advanced%20Guide.md
[5]:    https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop

[image-1]:	https://github.com/AckeeCZ/nodejs-cookbook/raw/master/raw/65692646.jpg "Brace Yourself!"
[image-2]:	https://github.com/AckeeCZ/nodejs-cookbook/raw/master/raw/health-00to19.png "BUM!"
[image-3]: https://github.com/AckeeCZ/nodejs-cookbook/raw/master/raw/DEg3cPZ.png