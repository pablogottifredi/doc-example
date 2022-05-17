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

Yo can see an example here

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















    Keep it simple and concise. Follow the DRY (Don’t Repeat Yourself) principle. You don’t need to comment on every single line of your code, use comments to explain something that really needs explaining and is not self-evident.
    Keep it up to date at all times. It’s best to document the code step by step, as it is written, instead of writing down the comments for the code that was written months ago. In doing so, you will save time and make the documentation precise and complete. Use proper versioning to keep track of all changes in the document.
    Document any changes to your code. Documenting new features or add-ons is pretty obvious. However, you should also document deprecated features, capturing any change in the product.
    Use simple language and proper formatting. Code documents are typically written in English so that any developer could read the comments, regardless of their native language. The best practices for documentation writing require using the Imperative mood, Present tenses, preferably active voice, and second person. Use consistent header, footer, headings, and font sizes for better readability.
    Combine automated documentation tools and human input. Automation will speed up the process, but a person can make the code documentation comprehensible while adding more of a personal touch.
