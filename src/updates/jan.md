# January 2023

------

## January 9th 2023 – *Update*

**TLDR;**
**Things Completed:** S3 API, Basic Neptune API to add, remove and update vertices. Plan for meal recommendations.
**Issues:** The JavaScript implementation of Apache Gremlin has holes in its implementation and a huge lack of documentation so have had difficult time with low level commands.
**Solutions:** Trialling different JavaScript implementations of Gremlin

Xav’s S3 API completed and working. Xav is now working on a dynamo API 
Will has basic Neptune working, he is now working on building the recommendation engine, we plan to use basic, non-ML collaborative filtering for the moment. This will consist of computing a cosine similarity matrix between all users which is a normalised value between 0 and 1 which determines how similar one user is to another; 1 being completely alike, 0 being not at all. We then determine how much a user may like a certain meal by multiplying all other user’s similarity values by how much each corresponding user likes that meal. We believe this is a good compromise for accuracy, time, and cost before we can transition to using ML powered recommendations.

---

## January 23rd 2023 – *Project Update*

**TLDR;** 
**Things Completed:** Initial static design of main meal card and quick meals meal cards, Recommendation Engine is now completed. Dynamo API also completed
**Issues:** AWS Cognito SDK not working, is also overly complicated for our use case. 
**Solutions:** Pivoting to use the AWS Amplify SDK instead as it provides higher level functions making implementing user authentication easier and faster.

Will has finished the meal recommendation engine using a cosine similarity matrix. Xav has finished the DynamoDB API and has both the DynamoDB API and the S3 API working from Lambda functions. George has finished the static meal cards.

Xav is now going to work on adding API gateway to access these Lambda functions from the client side. 
George is now going to be working on the Account and login pages. This will allow authenticated requests to be made from the client side to the lambda functions. Xav is also going to be helping George implement authentication via AWS Amplify

Will is now going to start on a web scraper to pull recipes from the internet. Recipes are factual therefore cannot be copyrighted themselves; we will remove any opinion or otherwise copyrightable material to ensure we can use them. 

