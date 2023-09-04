 # Stage 2 
 
I've broken this down into three goals

**Goal 1: Get the Azure function communicating with the database**
1. Create a new resource group for the API
2. Setup a Azure function using python
3. Create a Cosmos DB table (I did this via the portal)
4. Setup the bindings between the function and the database
5. The azure function needs to save a value to the table
6. Test the function (from the portal for now)
7. Setup the output bindings to return the  updated value from the function.

**Goal 2: Trigger the function from the outside world**
1. Setup the HTTP trigger for the function (use the portal for now)
2. When this works retrieve the url for the function and test it using an external API testing tool (I used Postman)

**Goal 3: Trigger the function from the static site**
If you get this working then the backend part is solved.
    
**Guides I used:**

- Installing python - https://developers.google.com/edu/python/set-up
- How to setup a Python Environment - https://www.freecodecamp.org/news/how-to-setup-virtual-environments-in-python/ 
- Azure Python SDK - https://learn.microsoft.com/en-us/azure/developer/python/sdk/azure-sdk-overview
- Azure Functions Python developer guide - https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-python
- Learn about different APIs - https://www.infoq.com/podcasts/api-showdown-rest-graphql-grpc/
- Learning about Javascript - https://developer.mozilla.org/en-US/docs/Web/JavaScript 
- Learning more JavaScript - https://www.codecademy.com/learn/introduction-to-javascript
- A guide to running Python tests - https://realpython.com/python-testing/
- JavaScript language overview - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Language_overview
- Learn how to make API calls with JavaScript - https://www.freecodecamp.org/news/how-to-make-api-calls-with-fetch
- Learn how to link CSS and JavaScript to HTML - https://betterprogramming.pub/link-css-and-js-files-with-html-file-f848d00b42e8 
- A CORS tutorial - https://auth0.com/blog/cors-tutorial-a-guide-to-cross-origin-resource-sharing/


