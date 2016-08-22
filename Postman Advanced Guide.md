# Postman advanced guide

## About

Postman is chrome extension for accessing REST API (or even sending forms and other things). Beside sending itself, it has some cool features but some of them are not that easy to discover and set up. This is what we can show you in this Guide! Cool stuff for cool things.

## Interceptor

One new feature is interceptor, where you can select, if you want to have Postman integrated with your Chrome or not. What's the difference? Well if you login to i.e. gmail, you then have URL address that looks like this https://mail.google.com/mail/u/0/#inbox and if you open that URL in another tab, you will still be logged in. Google Chrome also sends some more headers itself (i.e. accept-language header) which you do not want to send. Here is the interceptor, if it is off, chrome is not involved a you will not be logged in with that URL. If it is on, it is like sending requests from _another tab_.

## Collections
Create collection for every project and save every valuable query into it. You and your team will thank you later. It is also easily shareable via link.

## Environment variables

How to set up environment and environment variables you can find either yourself or on postman tutorial on the internet - it is intuitive and clear, but we will talk about more advanced usage.

Let's start at _where does we using it_? Well, everywhere where we can. Most of our requests look like this

![Image][image-1]

It allows you to have one collection that works with all environments - localhost, development, stage, production (or even more if you have more environments). The only change you have to do is to click and change the environment, which change the value of baseurl (and in this case, also userId).

### The power of scripts

You can run scripts after the request, they are _hidden_ in field tests, but you can do much more there. Especially defining new environment variables or rewrite them.

![Image][image-2]

Which in this case is this

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

You can use the body you have sent(requestData), you have received(responseBody) and even the existing variables(environment). For example in this case newly reqistered user properties are saved, therefore any operations will be with the new user. It also push previous user to user2 to test things between two users (i.e. one sending friendship to another) and it also remembers thing from request to i.e. test login with email and password.

The best advantage with this approach is, once you set it up, it is fully automatic. And because environment variables are saved, this state is preserved even when you restart your computer and run postman again. The users (or any other entities) you were working with are still the same.

[image-1]: https://github.com/AckeeCZ/nodejs-cookbook/raw/master/raw/postman01.png
[image-2]: https://github.com/AckeeCZ/nodejs-cookbook/raw/master/raw/postman02.png