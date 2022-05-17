# Purpose
This document try to defined the minimal documentation needed to transfer the code and the acceptances rules

## 1. Deployment Diagram & Architecture Diagram
Describe a visual diagram of any services pieces and dependencies. There are many techniques to do this, but if you follow the [UML deployment diagram]( https://en.wikipedia.org/wiki/Deployment_diagram) is an good approach.

Frequently the deployment diagram could have a similar aspect to architecture diagram, where you describe some context aspect (likes groups of services in same DMZ) or external services dependencies in other clouds.
You can combine de the deployment & architecture diagram in the same doc or design any diagram in separared files. The sense of this point is understand visually any dependency and configuration that could affect the normal function of a set of services

## 2. API Documentation
We prefer the API documented in OPEN API format https://swagger.io/specification/ a separated file (yml or json)
We undestand that the automated documentation is a good approach to solve this, but if that is the way, must be complete. Not only a repetitive way to describe "NAME of ROUTE and VERB", "This is a Name of ROUTE". Because, this is possible read directly from the code.

The usefull entris for the api documentation are:
- Group of mtehods
- Verb (put,
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
    - If the API are behind a authentication or authorization method, or front services that could add additional responses (for example 401 unautorized) you must include in the API documentation this response and their schema.
- Schemas
    - A list of any schema referenced in the documentation, to help to dev tools desing models, mocks and clients automatically. E.g. https://github.com/OpenAPITools/openapi-generator

Yo can see an example here https://github.com/pablogottifredi/doc-example/blob/main/openapi.example.json

Do you use automatic openapi generator? You can complete the fields


### 3. Code Documentation
A clean code must be enought to document it, only include a specific documentation (inside the code) if the process is to complex to understand their dependencies of if you have a portion of code with a business rule to solve hardest to follow.
Don't include documentation to explain patterns or the common structure of a project. E.g. DOT NOT INCLUDE //This is the controller.

### 4. Orquestation or coreography of Services
If you have a deocupled method to manage the services the complexity is when you need undestand wich sync process or messaging are used to communicate each domain.
If you use orquestation include an UML sequence diagram any time that a portion of code need runs several services dependencies to complete the transaction.
Additionally include if you have a monitor method to detect the fail of the transaction.
This documentation preferably is better in a separated file outside the code. You can use UML Sequence Diagram to represent it or any techniques that help you to explain ir.
If you use a coreography method is important to us, documents the name of any message and the list of listeners that runs.
If the services that you use had a user interfaces you can link it here. But if better if you have a separared document to help to developers to understand the transaction process

### 5. Deployment instructions
You have the entirely CI process solved? OK, the terraform (or other recipe project) is enought to include the documentation. Only you must have care that include a description of any variable in the recipe, and a way to indicates the steps to runs.

You have the CI uncompleted and need some process manually (specially in database migrations), include a deployment document instruction with any manual step that the devops must runs to install and include changes in the project.



## Best Practices
Keep it simple and concies. DRy (Don't repeat yourself)
The best practices recomends that you use English, but, if the times presses use your native language and ask for help to translate it in the next sprint. Is more important the existence of documentation before the shakespearean prose

Is you don't use any special platform to make the driagram, we recomends us diagram https://app.diagrams.net/ and provide the source file or if you are a warrior you can use the mermaid markdown support and include it in a md file https://github.blog/2022-02-14-include-diagrams-markdown-files-mermaid/
