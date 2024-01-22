1. Modernization with containers and serverless technologies

Background: App we build needs to scale quickly. to million of users, global availability, respond in milisecondds, handle petabytes of data.  

Modern applicatiion characteristics: Modular architectural patterns, as serverless as possible, agile development process; innovate faster and reducing risk time to market, and cost of ownership.  

what it means to be modular archictural patterns: the application decomposed into a number of smaller, independent component and loosely coupled microservices, each with its own dedicated data store.  

In microservices, services are typically built around business capabilities, independently deployable by fully deployment and machinery.  

diifferent services in a given application may actually be written in different programming languages, thus may also be usiing different data storage technologies.  

Benefits: Separating monolith into these smaller components makes it faster to release cadence, sdlc automation, flexible upgrades, and rollback scenarios, reusable services increase time to value of application, horizontal scaling based on actual demand, application portability.  


Traditional usage in AWS is using Amazon EC2, which is a virtual machine, and aws manages physical hardware, software, networking and facilities or we called it as Infrastructure as a service  

In contrast if we want to enable the serverless containers, we use AWS Fargate. The difference from the customer perspective, or say us the developers, AWS Fargate manages applicatioin code, data source integratiions, security-config and updates, network config and tasks management. In EC2 we manage application code, data source integrations, scaling, security config and updates, network config, and task management.  Aws fargates can manage scaling by clustering, contaiiner orchestration.  

So we can combined the containerization with fargate, and serverless with lambda.  While if we just want to have own authority, use EC2  

But the Containers and serverless has distinctions: Containers: compute-oriented, easily manage infrastructure, infrastructure consumption-based pricing. Serverless] Event-oriented, abstract away infrastructure, requesed-based pricing.  

Example of events: Iimage processiing when an object is uploaded to an S3 bucket, then you can use Lambda.  

