# Book Extra Chapters - U.2.6: Upgrade to Spring Boot 2.6.2, Spring Cloud 2021.0, and JDK 17

Good news! The book contents are still good and everything in there applies to the newest releases. If you don't have it yet, [get it now!](https://amzn.to/3nADn4q)

This repository contains the source code of the practical use case described in the book [Learn Microservices with Spring Boot (2nd Edition)](https://amzn.to/3nADn4q).

If you want to know more details about the book and its extra chapters, make sure to [visit this page](https://tpd.io/book-extra).

The book follows a pragmatic approach to building a Microservice Architecture, using a reference implementation that evolves from a small monolith to a full microservice system. 

## Upgrade - Spring Boot 2.6.2, JDK 17

This extra chapter brings the project dependencies to the latest Spring Boot, Spring Cloud, and Java versions. 

All these changes are described in detail in a [blog post](https://thepracticaldeveloper.com/book-update-2.6.2/) at The Practical Developer's website. Visit [https://thepracticaldeveloper.com/book-update-2.6.2/](https://thepracticaldeveloper.com/book-update-2.6.2/)

### Changes - migrating from Spring Boot 2.5.5 to 2.6.2

There are no additional changes needed in our codebase for this update apart from the version updates:

* All poms changed from 2.5.5 to 2.6.2
* Spring Cloud version now points to 2021.0.0
* Docker-compose file also points to the new generated images

#### Gateway: a minor remark

After this update, I see a long stacktrace in the Gateway with a message as follows:

```java
i.n.r.d.DnsServerAddressStreamProviders  : Unable to load io.netty.resolver.dns.macos.MacOSDnsServerAddressStreamProvider, fallback to system defaults. This may result in incorrect DNS resolutions on MacOS.
...        
Caused by: java.lang.UnsatisfiedLinkError: 'io.netty.resolver.dns.macos.DnsResolver[] io.netty.resolver.dns.macos.MacOSDnsServerAddressStreamProvider.resolvers()'
```

This is only relevant if you're running the project in MacOS. It seems this has been always there but its logging level was promoted and now we see it in the console. It doesn't have any impact on the running microservice.

For more details about this topic, see:

* https://github.com/netty/netty/issues/11020
* https://github.com/netty/netty/pull/10848

#### References

* [The blog post](https://thepracticaldeveloper.com/book-update-2.6.2/).

Some additional references from the official documentation:

* [Spring Boot 2.6 Release Notes](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.6-Release-Notes)
* [Spring Cloud 2021.0.0 Blog post](https://spring.io/blog/2021/12/02/spring-cloud-2021-0-0-codename-jubilee-has-been-released)
* [Spring Cloud 2021.0.0 Release Notes](https://github.com/spring-cloud/spring-cloud-release/wiki/Spring-Cloud-2021.0-Release-Notes)

## Running the app

You can use Docker to start the complete system, and you can also run the services one by one on your computer. [See the book's last chapter repository](https://github.com/Book-Microservices-v2/chapter08d) for the detailed instructions.

## Questions

* Do you have questions about how to make this application work?
* Did you get the book and have questions about any concept explained within this chapter?
* Have you found issues using updated dependencies?

Don't hesitate to create an issue in this repository and post your question/problem there. 

## About the book

Are you interested in building a microservice architecture from scratch? You'll face all the challenges of designing and implementing a distributed system one by one, and will be able to evaluate if it's the best choice for your project.

[Buy the book at Amazon](https://amzn.to/3nADn4q), or visit [https://tpd.io/book-extra](https://tpd.io/book-extra) for all the details.

### Purchase

You can **buy the book online** from these stores:

* [Amazon](https://amzn.to/3nADn4q)
* [Apress](https://www.kqzyfj.com/click-8535631-14029332?url=https%3A%2F%2Fwww.apress.com%2Fgp%2Fbook%2F9781484261309)
* and other online stores, check the IBAN (9781484261309) on [google](https://www.google.com/search?q=9781484261309)

### Source code by chapter (all repositories are available on Github)

* [Chapter 3. A professional 3-tier 3-layer Spring Boot app](https://github.com/Book-Microservices-v2/chapter03)
* [Chapter 4. Building a basic frontend in React (backender-friendly)](https://github.com/Book-Microservices-v2/chapter04)
* [Chapter 5. The Data Layer Concepts and Spring Data JPA](https://github.com/Book-Microservices-v2/chapter05)
* [Chapter 6. Starting with Microservices - Synchronous](https://github.com/Book-Microservices-v2/chapter06)
* [Chapter 7. Event-Driven Architectures - Making our system asynchronous](https://github.com/Book-Microservices-v2/chapter07)
* [Chapter 8 (I). The Gateway Pattern in Microservice Architectures (Spring Cloud Gateway)](https://github.com/Book-Microservices-v2/chapter08a)
* [Chapter 8 (II). Service Discovery and Load Balancing for Spring Boot Microservices (Consul / Spring Cloud Load Balancer)](https://github.com/Book-Microservices-v2/chapter08b)
* [Chapter 8 (III). Centralized Configuration with Consul KV](https://github.com/Book-Microservices-v2/chapter08c)
* [Chapter 8 (IV). Centralized Logs, Distributed Tracing, and Containerization with Docker (Buildpacks) and Docker Compose](https://github.com/Book-Microservices-v2/chapter08d)

Extra chapters:

* [E.1. End-to-End Microservice tests with Cucumber](https://github.com/Book-Microservices-v2/cucumber-tests)
* [U.2.4.0. Upgrade: Spring Boot 2.4.0 and more](https://thepracticaldeveloper.com/book-update-2.4.0/)
* [U.2.5.5. Upgrade: Spring Boot 2.5.5 and more](https://thepracticaldeveloper.com/book-update-2.5.5/)
* [U.2.6.2. Upgrade: Spring Boot 2.6.2 and more](https://thepracticaldeveloper.com/book-update-2.6.2/)
