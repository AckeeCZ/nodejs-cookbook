# Postman advanced guide

## About

Postman is chrome extension for accessing REST API (or sending forms and other things). Beside sending itself, it has some cool features!

There are lot tutorials/guides for postman and it is also intuitive in most use-cases, therefore I would like to focus on few _specialities_ rather than creating complete guide.

## Interceptor

One new feature is interceptor, where you can select, if you want to have Postman integrated with your Chrome or not. What's the difference? Well if you login to i.e. gmail, you then have URL address that looks like this _https://mail.google.com/mail/u/0/#inbox_ and if you put this URL in another tab, you will still be logged in. Google Chrome also sends some more headers itself (i.e. accept-language header) which you do not want to send. Here is the interceptor, if it is off, chrome is not involved a you will not be logged in with that URL. If it is on, it is like sending requests from _another tab_.

## Collections
Create collection for every project and save every valuable query into it. You and your team will thank you later. It is also easily shareable via link.

## Environment variables

Environment variables saves your time. Easy to use and set-up, huge benefits.

Let's start at _where does we using it_? Well, everywhere where we can. Most of our requests look like this

![Image][image-1]

It allows you to have one collection that works with all environments - localhost, development, stage, production (or even more).

### The power of scripts

You can run scripts after the request, they are _hidden_ in field _tests_, but you can do much more there. Especially defining new environment variables or rewrite them.

![Image][image-2]

This is the text-output of picture above:

```javascript
tests["Successful POST request"] = responseCode.code === 200 || responseCode.code === 201 || responseCode.code === 202;

if (tests["Successful POST request"]){
  var responseData = JSON.parse(responseBody);
  postman.setEnvironmentVariable('accessToken2', environment.accessToken);
  postman.setEnvironmentVariable('refreshToken2', environment.refreshToken);
  postman.setEnvironmentVariable('userId2', environment.userId);

  postman.setEnvironmentVariable('accessToken', responseData.credentials.accessToken);
  postman.setEnvironmentVariable('refreshToken', responseData.credentials.refreshToken);
  postman.setEnvironmentVariable('userId', responseData.user.id);
  
  var requestData = JSON.parse(request.data);
  postman.setEnvironmentVariable('userEmail2', environment.userEmail);
  postman.setEnvironmentVariable('userPassword2', environment.userPassword);  
  postman.setEnvironmentVariable('userEmail', requestData.email);
  postman.setEnvironmentVariable('userPassword', requestData.password);  
}
```

You can use the body you have sent(requestData), you have received(responseBody) and even the existing variables(environment). 

This takes the values of existing environment variables and writes them to another environment variables :
```javascript
  postman.setEnvironmentVariable('accessToken2', environment.accessToken);
  postman.setEnvironmentVariable('refreshToken2', environment.refreshToken);
  postman.setEnvironmentVariable('userId2', environment.userId);
```

Why do that? Well sometimes two users are interacting with each other - sending messages, accepting friendships etc. You need to have two different accounts to test it. Therefore you need two accesses and user info. We push previously created user to _user2_

This is getting info from response:
```javascript
  var responseData = JSON.parse(responseBody);
  postman.setEnvironmentVariable('accessToken', responseData.credentials.accessToken);
  postman.setEnvironmentVariable('refreshToken', responseData.credentials.refreshToken);
  postman.setEnvironmentVariable('userId', responseData.user.id);
```

Data comes in JSON - we parse it and use it.

The last part is taking data from request:

```javascript
  var requestData = JSON.parse(request.data);
  postman.setEnvironmentVariable('userEmail2', environment.userEmail);
  postman.setEnvironmentVariable('userPassword2', environment.userPassword);  
  postman.setEnvironmentVariable('userEmail', requestData.email);
  postman.setEnvironmentVariable('userPassword', requestData.password);  
```

The code above is related to registration and you want to remember email for i.e. login. And this is how our login URL look like in postman after all this :

```
{{baseurl}}/api/v1/auth/sign-in?username={{userEmail}}&password={{userPassword}}
```

Or when you creating friendship, this is how looks our request body

```javascript
{  
  "userIdReceiver" : "{{user2Id}}"
}
```

The best advantage with this approach is, once you set it up, it is fully automatic.

Dave is lazy. Dave set-up local environment to save time in future. Be like Dave.

[image-1]: https://github.com/AckeeCZ/nodejs-cookbook/raw/master/raw/postman01.png
[image-2]: https://github.com/AckeeCZ/nodejs-cookbook/raw/master/raw/postman02.png