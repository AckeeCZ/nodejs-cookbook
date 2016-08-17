# Best practices

## Table of Contents

## ESLint

![Image][image-1]

### About

ESLint is used for static control of quality of your code and for coding standards.

### How to use

Each project has scripts in package.json for running the eslint with all required parameters.

### Why do we use it

It is very easy to set up - either on your local machine either in continues integration process.

Also having same standards is always good and prevents a lot of potentional bugs.

### What rules do we use

We decided that we should look to succesfull companies to see, how they roll. We liked a lot an [airbnb javascript guide][1], therefore that was the starting point. We managed to go through each rule and decide if we want to follow it. Some points where changed (i.e. changed from error to warning), but most of it stayed same as theirs.

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

Most of you probably know automated testing. We also use it a lot, not having sufficient code coverage can be even reason to not accept your commit into development and/or production branch!

And worst of all, our continues integration system (jenkins at the moment) will mark your commit with __this evil picture__: ![Image][image-2]

### Why we use it

Writing tests in beggining of project seems like wasting time. You spend time with writing tests, while it almost never find any additional error. However as project continues, the complexity rises with incoming change-requests from customers (or mobile app/frontend developers, but you know, you are writing the server, you are the master, they have to obey your API).

Bigger the code and complexity, bigger the chance you create bug while fixing another or when implementing new feature. Everyone one at least once said : this new code should _never ever_ affect existing code but it actually __does__ (yes, life is cruel), good written tests are here for you to warn you.

### What tests do we use

In most of our node.js applications, we are focusing on integeration tests that are sending requests to our server. However for some more complex components, we do use _classic_ unit tests.

### Technologies

The [Mocha][2] with [Chai][3] are well supported and popular testing frameworks, therefore we decided to utry them and they serve its purpose.

### Code coverage

As mentioned in _about_ section, we do use code coverage tools, which tells you how good you are covering code with your tests. You can even see in web browser page which shows you all info you need, even marking the line which was tested and lines which was not.


## Version Control

We use git and gitlab. we follow [feature branch workflow][4] for development with merge requests. We have `master` branch where lays production code. in `development` branch we keep *current* development version of the app. 

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

[image-1]:	https://github.com/libor-vilimek/cookbook/raw/master/raw/65692646.jpg "Brace Yourself!"
[image-2]:	https://github.com/libor-vilimek/cookbook/raw/master/raw/health-00to19.png "BUM!"