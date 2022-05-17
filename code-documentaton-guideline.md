## Purpose
This document try to defined the minimal documentation needed to transfer the code and the acceptances rules

### Deployment Diagram & Architecture Diagram
Describe a visual diagram of any services pieces and dependencies. There are many techniques to do this, but if you follow the [UML deployment diagram]( https://en.wikipedia.org/wiki/Deployment_diagram) is an good approach.

Frequently the deployment diagram could have a similar aspect to architecture diagram, where you describe some context aspect (likes groups of services in same DMZ) or external services dependencies in other clouds.
You can combine de the deployment & architecture diagram in the same doc or design any diagram in separared files. The sense of this point is understand visually any dependency and configuration that could affect the normal function of a set of services

#### API Documentation
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
    -
    







    Keep it simple and concise. Follow the DRY (Don’t Repeat Yourself) principle. You don’t need to comment on every single line of your code, use comments to explain something that really needs explaining and is not self-evident.
    Keep it up to date at all times. It’s best to document the code step by step, as it is written, instead of writing down the comments for the code that was written months ago. In doing so, you will save time and make the documentation precise and complete. Use proper versioning to keep track of all changes in the document.
    Document any changes to your code. Documenting new features or add-ons is pretty obvious. However, you should also document deprecated features, capturing any change in the product.
    Use simple language and proper formatting. Code documents are typically written in English so that any developer could read the comments, regardless of their native language. The best practices for documentation writing require using the Imperative mood, Present tenses, preferably active voice, and second person. Use consistent header, footer, headings, and font sizes for better readability.
    Combine automated documentation tools and human input. Automation will speed up the process, but a person can make the code documentation comprehensible while adding more of a personal touch.
