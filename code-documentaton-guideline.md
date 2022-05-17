# Purpose
This document try to defined the minimal documentation needed to transfer the code and the acceptances rules

## 1. Deployment Diagram & Architecture Diagram
Describe a visual diagram of any services pieces and dependencies. 
There are many techniques to do this, but if you follow the [UML deployment diagram]( https://en.wikipedia.org/wiki/Deployment_diagram) is an good approach.

Frequently the deployment diagram could have a similar aspect to architecture diagram, where you describe some context aspect (likes groups of services in same DMZ) or external services dependencies in other clouds.

You can combine de the deployment & architecture diagram in the same doc or design any diagram in separated files. 
The sense of this point is understand visually any dependency and configuration that could affect the normal function of a set of services

## 2. API Documentation
We prefer the API documented in OPEN API format https://swagger.io/specification/ a separated file (yml or json)
We understand that the automated documentation is a good approach to solve this, but if that is the way, must be complete. Not only a repetitive way to describe "NAME of ROUTE and VERB", "This is a Name of ROUTE". Because is possible read it directly from the code.

The useful entries for the API documentation are:
- Group of methods (domain)
- Verb (put,patch,delete,post,get). This point is important because the API Gateway should open only the describe methods
- Route
- Description
- Parameters: 
    - Description
    - Kind (path, header, query)
    - Example value
- Body request schema (if apply)
    - Include an example of data that you could use in a test
- Authentication method
- Responses
    - A list of any code response with the real response schema of any case
    - If the API is behind an authentication or authorization method, or front services that could add additional responses (for example 401 unauthorized) you must include in the API documentation this response and their schema.
- Schemas
    - A list of any schema referenced in the documentation, to help to dev tools desing models, mocks and clients automatically. for example this tool: https://github.com/OpenAPITools/openapi-generator

You can see an example here https://github.com/pablogottifredi/doc-example/blob/main/openapi.example.json 

Do you use automatic openapi generator? You can complete the fields


## 3. Code Documentation
A clean code must be enought to document it, only include a specific documentation (inside the code) if the process is to complex to understand their dependencies of if you have a portion of code with a business rule to solve hard to follow.
Don't include documentation to explain patterns or the common structure of a project. E.g. DOT NOT INCLUDE //This is the controller.

## 4. Orquestation or coreography of Services
If you have a decoupled method to manage the services the complexity is when you need to understand which sync process or messaging is used to communicate each domain.
If you use orchestration include a UML sequence diagram any time that a portion of code need runs several service dependencies to complete the transaction.
Additionally include if you have a monitor method to detect the failure of the transaction.
This documentation preferably is better in a separated file outside the code. 
You can use UML Sequence Diagram to represent it or any techniques that help you to explain it.
If you use a choreography method is important to us, to document the name of any message and the list of listeners that runs.
If the message services that you use had user interfaces that help to see the list of messages you can link them here. 
But is better if you have a separate document to help developers to understand the transaction process

## 5. Deployment instructions
Do you have the entirely CI process solved? OK, the terraform (or another recipe project) is enough to include the documentation. Only you must have care that includes a description of all the variables in the recipe, and a way to indicate the steps to run.

If you have the CI uncompleted and need some process manually (especially in database migrations), include a deployment document instruction with any manual step that the DevOps must run to install and include changes in the project.

## 6. Readme in each project
Follow the template of (readme)[https://github.com/pablogottifredi/doc-example/blob/main/README.md] and include it in each project.


# Best Practices
Keep it simple and concise. DRY (Don't repeat yourself)
The best practices recommend that you use English, but if the time's pressed use your native language and ask for help to translate it in the next sprint. Is more important the existence of documentation before the Shakespearean prose

If you don't use any special platform to make the diagram, we recommend diagram it in https://app.diagrams.net/ and providing the source file in the repo.
If you are a warrior you can use the (mermaid markdown support)[https://github.blog/2022-02-14-include-diagrams-markdown-files-mermaid/]  and include it in a MD file 
