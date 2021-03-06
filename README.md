# Springy Store μServices

- This project is a development of a small set of Spring Boot based Microservices projects, that implement cloud-native intuitive, design patterns and coding best practices.
- The project follows [**CloudNative**](https://www.cncf.io/) recommendations and The [**twelve-factor app**](https://12factor.net/) methodology for building *software-as-a-service apps* to show how μServices should be built and deployed.
- The project is using cutting edge technologies like Docker, Kubernetes, Elasticsearch Stack for logging and monitoring, Java SE 14, MySQL database, MongoDB, TDD, unit, integration & performance testing and Reactive Programming, and many more.

------

I am developing this project as stages, and all such stages are documented under project **Springy Store μServices** [wiki page](https://github.com/mohamed-taman/Springy-Store-Microservices/wiki). each such stage will be a release so you can go back and forward between releases to see the differences and how adding things solve specific problems we face.

For example; in the first stage (1st release) I just created project structure, basic services skeleton, integration between them, and finally write integration testing as well as semi-automated testing for the whole services functionality.

At 1st stage the **recommendation** and **review** microservices generate local in-memory data and **product composite service** calls the other three services (*product*, *recommendation*, and *review*) statically to generate client aggregate response for a specific product. Therefore in: 

- The second stage I will introduce **database integration**, then in 
- The third stage I will introduce **Dockerization** of our services and **docker-compose**, and in 
- The fourth stage I will introduce **service discovery**, and so on.

## Getting started

The first stage aka (**Release v1.0**) is about creating and implementing a set of project Microservices.

### Creating a Set of Cooperating Microservices

The following topics are covered in this 1st stage (other stages topics will be documented in a project wiki):

- Introducing the microservice landscape.
- Generating skeleton microservices.
- Adding RESTful APIs.
- Adding a **product composite**, **product**, **recommendation**, and **review** microservices.
- Adding error handling.
- Testing the APIs manually.
- Adding automated tests of microservices in isolation.
- Adding semi-automated tests to a microservice landscape.

### System Boundary - μServices Landscape

![System Boundary](docs/stage1/app_ms_landscape.png)

### Required software

The following software pieces are initially required:

1. **Git**: it can be downloaded and installed from https://git-scm.com/downloads.

2. **Java 14**: it can be downloaded and installed from https://www.oracle.com/technetwork/java/javase/downloads/index.html.

3. **curl**: this command-line tool for testing HTTP-based APIs can be downloaded and installed from https://curl.haxx.se/download.html.

4. **jq**: This command-line JSON processor can be downloaded and installed from https://stedolan.github.io/jq/download/.

5. Spring Boot Initializer: This *Initializer* generates *spring* boot project with just what you need to start quickly! start from here https://start.spring.io/.

   > For each future stage, I will list the newly required software. 

Follow the installation guide for each software website and check your software versions from the command line to verify that they are installed correctly.

## Using an IDE

I recommend that you work with your Java code using an IDE that supports the development of Spring Boot applications such as Spring Tool Suite or IntelliJ IDEA Ultimate Edition. So you can use the Spring Boot Dashboard to run the services, run each microservice test case and many more.

All that you want to do is just fire up your IDE **->** open or import the parent folder `springy-store-microservices` and everything will be ready for you.

## Playing With Spring Store Project

### Cloning It

First open **git bash** command line, then simply you can clone the project under any of your favorite places as the following:

```bash
> git clone https://github.com/mohamed-taman/Springy-Store-Microservices.git
```

### Build & Test Them In Isolation

To build and run test cases for each service & shared modules in the project we need to do the following:

#### First: Build & Install Shared Dependencies

> This is done for the first time only or any new version of shared modules..

To build and install `store-utils`, `store-api`, `store-chassis`  libraries, from the root folder `springy-store-microservices` run the following commands:

```bash
mohamed.taman@DTLNV8 ~/springy-store-microservices 
λ ./setup.sh
```

and you should expect output like this:

```bash
mohamed.taman@DTLNV8 ~/Springy Store Microservices 
λ ./setup.sh

Installing all Springy store core shared modules
................................................

1- Installing shared [Utilities] module...
Done successfully.

2- Installing shared [APIs] module...
Done successfully.

3- Installing [parent project] module...
Done successfully.

Wooohooo, building & installing all project modules are finished successfully.
and the project is ready for the next step. :)
```

#### Second: Build & Test Microservices

Now it is time to build our **4 microservices** and run each service integration test in isolation by running the following commands:

```bash
mohamed.taman@DTLNV8 ~/springy-store-microservices 
λ cd store-chassis
mohamed.taman@DTLNV8 ~/springy-store-microservices/store-chassis
λ mvn clean verify
```

All build commands and test suite for each microservice should run successfully and the final output should be like this:

```bash
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary:
[INFO]
[INFO] Springy Store APIs 1.0-SNAPSHOT .................... SUCCESS [  3.048 s]
[INFO] Springy Store Utils 1.0-SNAPSHOT ................... SUCCESS [  2.107 s]
[INFO] Springy Store Chassis 0.0.1-SNAPSHOT ............... SUCCESS [  0.865 s]
[INFO] Product Composite Service 0.0.1-SNAPSHOT ........... SUCCESS [ 11.086 s]
[INFO] Product Service 0.0.1-SNAPSHOT ..................... SUCCESS [  9.795 s]
[INFO] Review Service 0.0.1-SNAPSHOT ...................... SUCCESS [  9.214 s]
[INFO] Recommendation Service 0.0.1-SNAPSHOT .............. SUCCESS [  9.288 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  46.006 s
[INFO] Finished at: 2020-04-01T17:07:52+02:00
[INFO] ------------------------------------------------------------------------
```

### Running Them

Now it is time to run all of them, and it is very simple just run the following two commands:

```bash
mohamed.taman@DTLNV8 ~/springy-store-microservices/store-chassis
λ cd ..
mohamed.taman@DTLNV8 ~/springy-store-microservices 
λ ./run-em-all.sh
```

All the services will run in parallel and their output will be printed to the console. 

### Testing Them All

Now it is time to test all functionality of the application as one part. and to do so just run the following automation test script:

```bash
mohamed.taman@DTLNV8 ~/springy-store-microservices 
λ ./test-em-all.sh
```

The result should be something like this:

```bash
Starting [Springy Store] full functionality testing....

HOST=localhost
PORT=9080
Test OK (HTTP Code: 200)
Test OK (actual value: 1)
Test OK (actual value: 3)
Test OK (actual value: 3)
Test OK (HTTP Code: 404, {"httpStatus":"NOT_FOUND","message":"No product found for productId: 13","path":"/product-composite/13","time":"2020-04-01@14:51:48.812+0200"})
Test OK (HTTP Code: 200)
Test OK (actual value: 113)
Test OK (actual value: 0)
Test OK (actual value: 3)
Test OK (HTTP Code: 200)
Test OK (actual value: 213)
Test OK (actual value: 3)
Test OK (actual value: 0)
Test OK (HTTP Code: 422, {"httpStatus":"UNPROCESSABLE_ENTITY","message":"Invalid productId: -1","path":"/product-composite/-1","time":"2020-04-01@14:51:49.763+0200"})
Test OK (actual value: "Invalid productId: -1")
Test OK (HTTP Code: 400, {"timestamp":"2020-04-01T12:51:49.965+0000","path":"/product-composite/invalidProductId","status":400,"error":"Bad Request","message":"Type mismatch."})
Test OK (actual value: "Type mismatch.")
```

### Closing The Story

And to close the story, we will need to shutdown Microservices manually service by service, hahaha just kidding, run the following script to shutdown them all:

```bash
mohamed.taman@DTLNV8 ~/springy-store-microservices 
λ ./stop-em-all.sh
```

 and the output should be as the following:

```bash
Stopping [Springy Store] μServices ....
---------------------------------------

Stopping Microservice at port 9080 ....
{"message":"Shutting down, bye..."}
Microservice at port 9080 stopped successfully ....

Stopping Microservice at port 9081 ....
{"message":"Shutting down, bye..."}
Microservice at port 9081 stopped successfully ....

Stopping Microservice at port 9082 ....
{"message":"Shutting down, bye..."}
Microservice at port 9082 stopped successfully ....

Stopping Microservice at port 9083 ....
{"message":"Shutting down, bye..."}
Microservice at port 9083 stopped successfully ....
```

### The End

Happy coding :)
