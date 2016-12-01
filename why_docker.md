# Why Docker
Docker is in general very cool in the sense that, once you have learned it, Docker makes application development easier. Don't take my word for it though, here is what is says in the [Haufe Docker Style Guide Introduction](https://github.com/Haufe-Lexware/docker-style-guide){:target="_blank"}.

# Why Docker @ Haufe Group

To give you an idea why we want to use Docker at Haufe Group, let's take a look at one of our projects - Next Best Action. Our marketing departments are looking to move away from classical push marketing because they don't believe they can really understand our customers with classical marketing techniques.  To understand our customers, Haufe Group wishes to be able to predict how our customers' behave. To predict this behavior better, we want to know which action our customers take when they visit our systems. Through their actions, it may be possible to detect "action patterns" that tend to result in a particular outcome like buying a Haufe Group product. This action-data adds to the "customer profile" and helps our marketing colleagues better understand what our customers want. 

There are a lot of enterprise software packages out there to do get this kind of data. But, after marketing reviewed several different applications, there wasn't enough buy in from the various marketing groups to make a "buy decision" at the enterprise level. The costs were too high, the feature set too big, and Haufe Group would never get enough value. 

Marketing still wanted to get this data, and so, instead of buying an enterprise software that has high costs and an uncertain value proposition, they decided to try to build an application that would cost little and that adds value as it grows. Enter Docker. Haufe Group doesn't need docker to create a prototype application, but by using Docker, you can do the following:
* Locate, compose and run single applications
* Compose and run multiple applications to work together as services
* Persist and reuse these composed applications and services and reuse them in other environments
* Automate integration and deployment of applications and services as immutable applications







