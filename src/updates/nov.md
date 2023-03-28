# November 2022


## November 9th 2022 – *First Meeting*

------


**TLDR;**
- **Things Completed:** Initial Infrastructure plan and design ideas 
- **Issues:** Figuring out how to implement meal recommendations and what databases we will need
- **Solutions:** AWS’s Graph Database, Neptune. 

We have decided on and initial infrastructure and planned how features are going to work.
Our current infrastructure plan is as follows: Kubernetes ran on Fargate through EKS for computing. These Kubernetes will contain code to access databases and compute meal recommendations. Our databases will be Neptune for user and meal relationships, DynamoDB for storing simple key-value data pairs and then Redshift for storing metadata for analytics. 

We are currently working on learning how to use Kubernetes, how we need to lay out data in the databases, and how to interact with the databases.



## November 16th 2022 – *Revising Infrastructure*

------


**TLDR;**
- **Things Completed:** A new revision of infrastructure and a deeper understanding of database layout.
- **Issue:** What infrastructure to use
- **Solution:** Kubernetes are not needed as our system is not big enough plus they are expensive, can use Docker containers with ECS and Fargate on AWS.

After looking over our current infrastructure, we realised that using Kubernetes would be more effort than it would be worth. Our system was not yet big enough or distributed enough to require Kubernetes. Originally, taking inspiration from how SnapChat’s infrastructure works, we were going to use Kubernetes ran on AWS Fargate through EKS. We found very quickly that this was going to be very expensive but also extremely time consuming to not only set up but also teach ourselves how to use Kubernetes. To save this time and money we are now looking at using Docker containers ran on AWS Fargate though ECS/ECR.

## November 30th 2022 – *General update*


------

**TLDR;** 
- **Things Completed:** Initial static design of main meal card and quick meals meal cards
- **Issues:** Ran into front-end issues with meal cards moving more on Android devices
- **Solutions:** Solved by …

Will is currently working on interacting with Neptune and getting a basic API to work. Xav is working on creating an API to interact with AWS S3. George has begun coding the main feature of the app such as, the meal cards for the explore page and quick meals.
We will be doing less work for the following month as we have exams.

