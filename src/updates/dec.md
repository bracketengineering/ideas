# Decmeber 2022


## December 21nd 2022 – *Revising infrastructure*

-----

**TLDR;**
**Things Completed:** Revision of Technical plan
**Issues:** AWS Fargate and Redshift will be too expensive
**Solutions:** Using AWS Lambda instead of Fargate, and using S3 to store metadata instead of in redshift

After going over our use case and what services we need, we realised we had underestimated the size of data we would need, but more importantly, the full costs of using a big enough system with Fargate and Redshift. The costs from using Fargate with ECS and Redshift Serverless would cost anywhere from \$500 to \$300 USD per month (depending on how many containers run on Fargate and how many hours we need to use Redshift for) 
This is far beyond our budget, so we decided the best balance between performance and cost is AWS Lambda and S3. We will store user metadata in S3 so that it can be used later for customer analytics. AWS Lambda will provide us with very cheap, easy to use and access compute power for the simple requests that will be coming into our infrastructure. 

Any other additional computing power we need will be completed using short lived EC2 instances. Examples of this could be calculating customer analytics, calculating meal recommendations, or any other internal computing we need doing.

We will all be taking a short break over the Christmas and New Year Period

