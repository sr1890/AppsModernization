
# 12 APPS Modernization Principals

Below are the 12-factor principles

1) Codebase (One codebase tracked in revision control, many deploys)
	
	Twelve-factor app advocates of not sharing the code between the application. If you need to share you need to build a library and make it as a dependency and manage through package repository like maven.
	
	
2) Dependencies (Explicitly declare and isolate the dependencies)

	It talks about managing the dependencies externally using dependency management tools instead of adding them to your codebase.
	maven gradel 
	
	In non-containerized environments, you can go for configuration management tools like chef, ansible, etc. to install system-level dependencies.
	For a containerized environment, you can go for dockerfile.
	
	
3) Config (Store configurations in an environment)
	
	Anything that varies between the deployment environments is considered as configuration. This includes:
	
	Database connections and credentials, system integration endpoints
	Credentials to external services such as Amazon S3 or Twitter or any other external apps
	Application-specific information like IP Addresses, ports, and hostnames, etc.

4) Backing Services (treat backing resources as attached resources)

	As per 12 factor app principles, a backing service is an application/service the app consumes over the network as part of its normal operation. Database, Message Brokers, any other external systems that the app communicates is treated as Backing service.

	12-factor app can automatically swap the application from one provider to another without making any further modifications to the code base. Let us say, you would like to change the database server from MySQL to Aurora. To do so, you should not make any code changes to your application. Only configuration change should be able to take care of it.

5) Build, release, and Run (Strictly separate build and run stages)
	
	The application must have a strict separation between the build, release, and run stages. Let us understand each stage in more detail.

	Build stage: transform the code into an executable bundle/ build package.

	Release stage: get the build package from the build stage and combines with the configurations of the deployment environment and make your application ready to run.

	Run stage: It is like running your app in the execution environment.

	You can use CI/CD tools to automate the builds and deployment process. Docker images make it easy to separate the build, release, and run stages more efficiently.
	
6) Processes (execute the app as one or more stateless processes)
	
	As per 12-factor principles, the application should not store the data in in-memory and it must be saved to a store and use from there. As far as the state concern, your application should store the state in the database instead of in memory of the process.
	
	Avoid using sticky sessions, using sticky sessions are a violation of 12-factor app principles. If you would store the session information, you can choose redis or memcached or any other cache provider based on your requirements.
	
	Microservices: By adopting the stateless nature of REST, your services can be horizontally scaled as per the needs with zero impact. If your system still requires to maintain the state use the attached resources (redis, Memcached, or datastore) to store the state instead of in-memory.
	

7) Port Binding (Export services via port binding)
	
	In short, this is all about having your application as a standalone instead of deploying them into any of the external web servers.Microservices: Spring boot is one example of this one. Spring boot by default comes with embedded tomcat, jetty, or undertow.
	
	
8) Concurrency (Scale out via the process model)
	
	This talks about scaling the application. Twelve-factor app principles suggest to consider running your application as multiple processes/instances instead of running in one large system. You can still opt-in for threads to improve the concurrent handling of the requests.
	
	In a nutshell, twelve-factor app principles advocate to opt-in for horizontal scaling instead of vertical scaling.
	
	
9) Disposability (maximize the robustness with fast startup and graceful shutdown)

	The twelve-factor app s processes are disposable, meaning they can be started or stopped at a moment s notice. When the application is shutting down or starting, an instance should not impact the application state.

	Graceful shutdowns are very important. The system must ensure the correct state.The system should not get impacted when new instances are added or takedown the existing instances as per need. This is also known as system disposability.
	
	Microservices: By adopting the containerization into the deployment process of microservices, your application implicitly follows this principle at a maximum extent. Docker containers can be started or stopped instantly. Storing request, state, or session data in queues or other backing services ensures that a request is handled seamlessly in the event of a container crash.
	
10) Dev/prod parity (Keep development, staging, and production as similar as possible)

	The twelve-factor methodology suggests keeping the gap between development and production environment as minimal as possible. This reduces the risks of showing up bugs in a specific environment.

11) Logs (Treat logs as event streams)
	
	Logs become paramount in troubleshooting the production issues or understanding the user behavior. Logs provide visibility into the behavior of a running application.

	Twelve-factor app principles advocate separating the log generation and processing the log's information. From the application logs will be written as a standard output and the execution environment takes care of capture, storage, curation, and archival of such stream should be handled by the execution environment.
	
	Microservices: In Microservices, observability is the first-class citizen. Observability can be achieved through using APM tools (ELK, Newrelic, and other tools) or log aggregations tools like Splunk, logs, etc.
	
12) Admin processes (Run admin/management tasks as one-off processes)

	There is a number of one-off processes as part of the application deployment like data migration, executing one-off scripts in a specific environment.

	Twelve-factor principles advocates for keeping such administrative tasks as part of the application codebase in the repository. By doing so, one-off scripts follow the same process defined for your codebase.

Source: 

https://medium.com/techmonks/12-factor-app-principles-and-cloud-native-microservices-a383f6abc97f

