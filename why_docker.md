# Why Docker

Docker is in general very cool in the sense that, once you have learned it, Docker makes application development easier. Don't take my word for it though, here is what it says in the [Haufe Docker Style Guide Introduction](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/StyleGuideHome.md). Once again, Docker provides its own documentation and their [use cases are here](https://www.docker.com/use-cases).  
Some more uses cases for software developers can be found on [Romin Irani's blog](https://rominirani.com/docker-use-cases-ca12afba75b0#.1112htwem).

## Why Docker @ Haufe Group

To give you an idea why we want to use Docker at Haufe Group, let's take a look at one of our projects - Next Best Action. Our marketing departments are looking to move away from classical push marketing because they don't believe they can really understand our customers with classical marketing techniques.

**Editor's Note: We will want to add more use cases as they arise, list them and link them separately. For each use case there ought to be more examples and so on.**

## Marketing needs to know more

To understand our customers, Haufe Group wishes to be able to predict how our customers behave. To predict this behavior better, we want to know which action our customers take when they visit our systems. Through their actions, it may be possible to detect "action patterns" that tend to result in a particular outcome, like buying a Haufe Group product. This action-data adds to the "customer profile" and helps our marketing colleagues better understand what our customers want.

## Enterprise software was too much money, functionality...

There are a lot of enterprise software packages out there to get this kind of data. But, after marketing reviewed several different applications, there wasn't enough buy in from the various marketing groups to make a "buy decision" at the enterprise level. The costs were too high, the feature set too big, and Haufe Group would never get enough value.

## Starting small with Docker

Marketing still wanted to get this data, and so, instead of buying an enterprise software that has high costs and an uncertain value proposition, they decided to try and build an application that would cost little and that adds value as it grows. Enter Docker. While Haufe Group could have built a prototype application without Docker, by using Docker, the following was easier:

* Locate, compose and run single applications
* Compose and run multiple applications to work together as services
* Persist, transport and reuse these composed applications and services for different purposes
* Automate integration and deployment of applications and services as immutable infrastructure

And, of course, using Docker makes it easier to scale out instances of successful applications at a much lower cost then bare-metal-based or current hypervisor-based infrastructure.

## If it works, great! if not, no problem!

So one reason why Haufe Group is interested in Docker technology is that when it is unclear if we should "build or buy" or if "buy" is too expensive, it allows us to develop, test and deploy prototypes,  reach decisions, and move along fast. This technique helps to develop business value at reasonable cost. If the prototype must go to production, Docker helps us to develop, test, build, and deploy production applications over a continuous delivery pipeline and to scale these applications in the production environment. And, even if it doesn't work out, Haufe Group learns a lot about its business needs, and,  it wasn't that much work either. Here's how.

