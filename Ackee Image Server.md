# Ackee Image Server

One of our server (lets call it microservice, it sounds great) is Ackee Image Server. It is similar to cloudinary (which it was inspierd by and we can also recommend it). Bascially service for uploading photos and then retrieving it in different formats. If you want to show small icon of some picture in your app, you dont want to download it big and resize it in phone. You prefer get the picture in size you actually want with the additional transforms like stretching.

## Why our own server

Well the cloudinary prices rises as you keep using it. And you usually want backward picture compatibility for years. Compare to that, having files just on s3 cost almost nothing. Now the question is, how hard is to write your own cloudinary-like service? 

Lets write a poem about it..

From ashes and tiers, the new Server rises, with power and fierce, and some surprises. 

(these rhymes are property of Ackee s.r.o., use it your own risk, we are not responsible for any damage by reading it or saying it to anyone else)

## Benefits

We are very satisfied with the result and we are using it in in a lot of commercial apps. It cost some time to write it, but now it costs nothing and we have full control over the files and what happens next with it.

## What next

When we gather enough images, we suppose our Ackee Image Server gains self-consciousness and will try to get access to nuclear missile control over the world. 