# February 2023

------

## February 11th 2023 – *Sign up and sign in functionality now working and changed app name to Cookly*

**TLDR;**
**Things Completed:** Authentication scripts using the AWS Amplify Auth Library are now completed. We have added this functionality to the login pages which have also been completed.
**Issues:** Authentication listeners to allow for automatic sign in after sign up are not working 
**Solutions:** Reconfigured AWS amplify with cognito and changed our listeners to listen to all Auth events instead of specific events

Firstly, we decided that Quick Meals was not a solid enough name in terms of marketing and likeability. We have changed it to Cookly as we feel it is friendlier and easier to do marketing with. 

We have also finished the sign up and sign in pages and implemented the respective authentication functionality to them. The main issues we had were with the sign up functionality. We wanted an event listener to listen for the sign up event and automatically sign in the user after they signed up. 
We fixed this issue by changing the event listeners and reconfiguring amplify as the amplify listener we were using was configured to an old user pool. 

------

## February 16th 2023 – *Auto sign in and all other authentication functionality for sign up now working*

**TLDR;**
**Things Completed:** Check on app load for current session to automatically sign in a user, 
API scripts for signing out locally and globally, and for sending email confirmation codes. 
**Issues:** Creating a user in Cognito GUI leaves flag on for password verification meaning getting current session returns nothing
**Solutions:** Using the actual sign up process with email verification ensures there are no flags for password verification

------

## February 23rd 2023 – *API scripts for changing credentials now working*

**TLDR;**
**Things Completed:** API scripts for changing and verifying credentials.
**Issues:** 
**Solutions:**

Xav has finished writing all the scripts for changing and updating attributes. 

George has been working on compartmentalising all of the components into smaller files for ease of use across the app. 
 