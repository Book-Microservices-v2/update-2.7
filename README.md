# Book Extra Chapters - U.2.7: Upgrade to Spring Boot 2.7.1

This repository contains the source code of the practical use case described in the book [Learn Microservices with Spring Boot (2nd Edition)](https://amzn.to/3nADn4q).

If you want to know more details about the book and its extra chapters, make sure to [visit this page](https://tpd.io/book-extra).

The book follows a pragmatic approach to building a Microservice Architecture, using a reference implementation that evolves from a small monolith to a full microservice system. 

## Upgrade - Spring Boot 2.7

This extra chapter brings the project dependencies to the Spring Boot 2.7.1 version.

All these changes are described in detail in a [blog post](https://thepracticaldeveloper.com/book-update-2.7.1/) at The Practical Developer's website. Visit [https://thepracticaldeveloper.com/book-update-2.7.1/](https://thepracticaldeveloper.com/book-update-2.7.1/)

### Major H2 upgrade with Spring Boot 2.7

The Spring Boot 2.7 release has upgraded H2 to a new major version, 2.x. Many changes are backwards incompatible and two of them break our code.

#### Feature not supported: "AUTO_SERVER=TRUE && DB_CLOSE_ON_EXIT=FALSE"

These two features can't be used together anymore. See the [blog post](https://thepracticaldeveloper.com/book-update-2.7.1/) for more details.

Solved by removing the `DB_CLOSE_ON_EXIT` parameter from the connection URL.

#### Error executing DDL "create table user ..."

More detailed error:

```java
Caused by: org.h2.jdbc.JdbcSQLSyntaxErrorException: Syntax error in SQL statement "create table [*]user (id bigint not null, alias varchar(255), primary key (id))"; expected "identifier"; SQL statement: [...]
```

Reason: `user` is now a keyword, so it conflicts with the table name.
Fix (one of the possibilities): Add `NON_KEYWORDS=USER;` to the connection URL for the multiplication microservice's database.

See the [blog post](https://thepracticaldeveloper.com/book-update-2.7.1/) for a complete explanation.

## New configuration approach (changed in 2.4)

In addition to the mandatory upgrades to make the code work with 2.7, I also switched to the new configuration approach introduced by Spring Boot 2.4.x.

Required changes to move to the new configuration approach in 2.4:

* Remove the legacy bootstrap starter (if previously added, in my case it was)
* Remove the `bootstrap.properties` or `bootstrap.yml` and move all those properties to the `application.properties` or `application.yml`.
* For Spring Cloud Consul to work fine, add a `spring.config.import=consul:` property (or the YAML equivalent) to the projects using Consul.
* We can remove all the `test.properties` files and the `@TestPropertySource` annotation pointing to it that we needed to add for backwards compatibility with the bootstrap legacy mode.

All the details [here](https://thepracticaldeveloper.com/book-update-2.7.1/)

## Bonus: using an H2 server instead of an auto-server

This version also includes an H2 server Docker image so the microservices can use H2 as an isolated database server instead of using the shared database files offered by the `AUTO_SERVER` mode.

Check the [blog post](https://thepracticaldeveloper.com/book-update-2.7.1/) for the instructions.

## Bonus: remove the ugly error related to MacOS DNS resolver for Netty

To remove this error for good, I added the native DNS dependency for my local setup. This applies to the `gateway` service's `pom.xml`:

```xml
<dependency>
    <groupId>io.netty</groupId>
    <artifactId>netty-resolver-dns-native-macos</artifactId>
    <!-- Change this if your Mac is not M1, see e.g. https://stackoverflow.com/questions/65954571/spring-boot-2-4-2-dns-resolution-problem-at-start-on-apple-m1 -->
    <classifier>osx-aarch_64</classifier>
    <version>4.1.78.Final</version>
</dependency>
```

### Changes - migrating from Spring Boot 2.6 to 2.7

There are no additional changes needed in our codebase for this update apart from the version updates:

* All poms changed from 2.5.5 to 2.6.2
* Spring Cloud version now points to 2021.0.0
* Docker-compose file also points to the new generated images

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
* [U.2.7.1. Upgrade: Spring Boot 2.7.1 and more](https://thepracticaldeveloper.com/book-update-2.7.1/)
