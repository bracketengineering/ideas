# March 2023

---

## March 1st 2023: All Low Level Backend APIs now configured as a class and all page design finished

**TLDR;**
- **Things Completed:** Converted the Dynamo, S3 and Neptune APIs to classes, all front end page design has been finished
- **Issues:** 
- **Solutions:**

We have converted the Dynamo, S3 and Neptune APIs to classes for ease of use and interoperability. It makes it far easier and neater to use in our Lambda functions. We will use these Classes via Layers in our Lambda functions

All low level backend classes should be used as outlined in the following:

```JavaScript
/*
Class Names:
    dynamoDBClient for Dynamo
    s3Client for S3
    NeptuneClient for Neptune
*/
import ClassName from '/Layers/ClassName'

const class = new ClassName();

//promise
class.method(params)
    .then((result) => ...)

//async 
await class.method(params);
// then code to deal with result
```


---

## March 5th 2023 – Completed website

**TLDR;**
- **Things Completed:** Landing page, Team about page, and Cookly page are completed
- **Issues:** 
- **Solutions:**

The landing page is a simple page with navigation links. The Team page just gives an overview who we all are and what our respective roles are within the company. The cookly page gives a product overview of the app; we are waiting on infographics from George to finish that bit completely

---

## March 10th 2023 – Code for Lambda functions now completed

**TLDR;**
- **Things Completed:** High level lambda functions are now complete.
- **Issues:** 
- **Solutions:**

---

## March 14th 2023 – Cognito Authentication APIs and front end converted to a class

**TLDR;**
- **Things Completed:** Cognito API simplified and converted to a class. API caller class made for calls to lambda functions
- **Issues:** 
- **Solutions:** 

Makes it far easier for George to implement authentication. Enables far easier error handling as the async functions are dealt with in the class. Amplify’s Auth Library is used to get the current user meaning George has to submit less information into the function calls leaving less room for error. 
The Cognito class should be instantiated and used like the following:
```JavaScript
import CognitoAPI from '/apiScripts/amplify/CognitoAPI'

const cognito = new Cognito();

//promise
cognito.method(params)
    .then((result) => ...)
```


The API Caller class was created to enable extremely easy integration into the front end components. The API Caller class should be instantiated and used like the following.

```JavaScript
import APICaller from '/apiScripts/apiCalls/apiCaller'

const api = new APICaller();

//promise
api.method(params)
    .then((result) => ...)

//async 
await api.method(params);
// then code to deal with result
```

The API Caller Methods use a private `#genericCall` function (outlined below) to make the actual request to the respective API endpoint. Each method submits the type of request (get or set), the endpoint path of the request, and the payload data for the request. This structure allows for the most compact class and method input size as possible.

---

## March 19th 2023 – Web Scraper for recipes redone

**TLDR;**
- **Things Completed:** The web scraper has been redone to work with more websites
- **Issues:** We were restricted to using only one website with the original 
- **Solutions:** We have made the webscraper more general purpose so that it works with more websites

---

## March 21st 2023 – Issue Loading data from S3 into FlatList and Global colour scheme implemented

**TLDR;**
- **Things Completed:** Lambda functions for rating meals, saving meals, and signing up users getting. The API Caller class has been expanded to accommodate these new lambdas.
- **Issues:** When creating a FlatList in the front end the way we were calling the back end was not working 
- **Solutions:** Promises, useEffect, flat list render function

We have added lambda functions for rating meals, saving meals and signing up new users. The signing up users lambda function signs up a user via Amplify to Cognito but also creates a user node in Neptune and also sets a custom Cognito attribute as the Neptune ID so we can use the Neptune ID when making requests to the backend.

We had a set-back of around a day as the way we were rendering items in the flat list was not working with our async API calls. We also had a huge issue with using asynchronous calls within React Native components, so we decided to change to using promises. Instead of waiting for a function to return the actual promise before the next piece of code could be executed using async/await, which React Native does not like, Promises just return the promise object which `.then()` can then access but only when a promise has been returned. 

Using promises works far better and much more consistently with React Native and it also allows for parallel API calls instead being restricted to only using sequential calls. This will allow us to massively decrease the response times of the app.

--- 

## March 22nd 2023 – Error Message information not being returned from async function correctly

**TLDR;**
- **Things Completed:** Most methods in the API caller class have been implemented. George has finished the redesign of the main meal card
- **Issues:** Errors being returned from try/catch blocks are not being displayed correctly in the front end
- **Solution:** Using promises ensures that errors are caught and can be returned so they can be shown on the screen.

We implemented all of the main back end functionality into the front end. Images and text are all displayed correctly. The main issue we have run into is errors from Cognito not being displayed properly when returned via a try/catch async block. We found the solution to this was using a promise.

Here is an example of the before and after:


```JavaScript
//BEFORE
async signIn(username, password) {
    try {
        const user = await Auth.signIn(username, password);
        return user;
    } catch (error) {
        console.log("error signing in", error);
        return 0;
    }
}
//AFTER
async signIn(username, password) {
    return new Promise(async (resolve, reject) => {
       try {
         const user = await Auth.signIn(username, password);
         resolve(user);
       } catch (error) {
         reject(error);
       }
     });
}
```

Rejecting the error via a promise allows us to display the error message on screen along with red outlining of the text input box where there was an error.

--- 

## March 24th  2023 – Wrong structure of Neptune graph and database infrastructure

**TLDR;**
- **Things Completed:** 
- **Issues:** Our current database infrastructure was poorly designed for easily adding features in the future, and the addition of machine learning infrastructure
- **Solutions:** Redesign our infrastructure to rely more on Neptune and redesign how we connect data

We have realised that the way we have configured our database infrastructure does not work well for when we want to add new features or ML capabilities. We would have to redo large parts of the system and large parts of the data would have to be duplicated as it is not connected correctly. Therefore, the best solution to this was to redesign Neptune. We are going to have virtually all data in Neptune except user and app metadata which will be stored in S3, and … in Dynamo DB

We will store, users, meals, and ingredients as nodes in Neptune, with the links between each node representing how they are related. See below for a more detailed overview

![Neptune Structure](neptune_structure.png)

Reconfiguring the Neptune API we already have will not take too long as we just have to change which nodes and edges we are using, and not much of the underlying logic. This new structure also allows for a large performance increase as we can get virtually all the information we need from the graph in a single query. Moreover, as the graph scales, querying the database remain extremely fast. It also makes it extremely easy to add functionality for new features as we can just connect into to pre-existing data and relationships.  

The final benefit of this is the ease of use of Neptune ML. With all our data and relationships being stored in the same place, it makes using machine learning far easier and much more accurate. Using Neptune ML with a relationship rich graph will greatly improve how we recommend meals to users and will allow a greater depth and mix of prediction types. We will also be able to use Neptune ML for future features such as ingredient substitution.

---

## March 29th 2023 – Major updates

**TLDR;**
- **Things Completed:** Internal Docs have been updated to reflect all our changes, recipe walk through design completed
- **Issues:**
- **Solutions:**
