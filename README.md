# ddocker
Distributed Docker, share your docker images from any docker daemon.


# What is this?

This is the repo that will (eventually) hold the code for Distributed Docker, a service that allows to desentralize docker images. Instead of telling how cool (or not) this project might be, I prefer to ennumerate the use cases that I believe originated this: 

- Did it even happen to you that you needed to deploy code to prod by pushing docker images to a centralized registry that wasn't available?

- Have you ever made a presentation that required you to  push / pull a docker image that you wanted to share with the audience or use somewhere else and you found out that the inet connection is not working at all?

- Sometimes when you need to scale up an app you already have tons of daemons running the same version of the app that you want the scale. Why it is necessary to use outbound bandwith (not always), deal with possible connection errors if you already have daemons serving that image right next to you?.

- When pulling images from a swarm all daemons will try to fetch them concurrently from the same repository. If the swarm is already a cluster, wouldn't it make sense if the daemons 

- If you have a really poor upload speeds (like in our country) and you need to share docker images with your team members but you want to skip the burden of running and configuring

- INSERT YOUR USE CASE HERE (please submit PR's)



# How this did started?

Originally we were thinking of using the bittorrent protocol to distribute docker layers in a desentralized way using trackerless DHT protocol, but for different reasons (too many to type) we decided to use a different and simpler approach. 

# How does it work?

You can run ddocker in any current docker dameon without any modifications. You just run a container that mounts the daemon socket and credentials if necessary and ddocker will automatically expose an API that allows to retrieve the images that the daemon currently holds. So, instead of pulling an image from a registry you just do `docker pull somedaemon/image` and that's it.
ddocekr will "emulate" a registry API and calculate the layer hashes and serve them as necessary. As the layer hashes won't change, you will be able to use the native caching transparently

# What's the status of the proejct?

Originally my idea was to present this as a [Cool Hack](https://blog.docker.com/2016/05/dockercon-cool-hack-challenge/) for the DockerCon 2016 challenge, but unluckily it didn't get elected. It's not in my priorities to dedicate many hours to this ATM but hopefully, if it gets attraction, I will be able to present it some day. 

# FAQ

## Will this ever be released?

Hopefully, I have mostly working but it's poorly coded and full of nasty stuff everywhere. I just need to find the bandwidth to polish.

## What about security?

I'm sure many Sec experts might be thinking "this is completely wrong!". Yeah..  insecure as it bypases all the registry security implications, but it's a proof of concept. If it gets adoption I guess I'll have to deal with that eventually.

## Can I help?

Definitely, as the code is not ready yet I encourage you to open issues and discuss about possible tech definitions as well as other use cases. 



[&nbsp;](http://maintainerati.org/ "Mainteinerati")
