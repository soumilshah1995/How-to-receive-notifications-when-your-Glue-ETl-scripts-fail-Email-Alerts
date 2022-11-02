# How-to-receive-notifications-when-your-Glue-ETl-scripts-fail-Email-Alerts

![image](https://user-images.githubusercontent.com/39345855/199550250-5fb8e90d-6855-4e89-a038-d51f124f556d.png)

* Set up a job alert to notify you each time your job succeeds or fails if you're concerned about the status of your Glue job and are weary of constantly checking the job console for problems or success. Today, we'll put up a mechanism for notifications that will let us know when one of our Glue jobs has failed or halted.



---------------------------------------------------------------------
#### Solution:
* Whenever the state changes for glue job that event shall be sent to AWS Event Bridge and where we shall have a rule if the event matches with given rule then event shall be passed to Lambda function which will process and send details to SNS Topic where subscribed candidates can be notified via email 

#### Steps to use 

##### Step 1: Download the repository

##### Step 2: change the Env Values 
```
ACCOUNT=XXXXX
TopicName=glue-jobs-topics


DEV_ACCESS_KEY=XXXXXXXXX
DEV_SECRET_KEY=XXX
DEV_REGION=us-east-1


```

* replace where it says XXXX with your AWS Account ID

##### Step 3: Add your Email Address

```
    MySubscription:
      Type: AWS::SNS::Subscription
      Properties:
        Endpoint: <ADD YOUR EMAIL ADDRESS HERE>
        Protocol: email
        TopicArn: !Ref 'SNSTopic'
```


##### Step 4 Deploy

```
serverless config credentials --provider aws --key <ACCESS KEY>  --secret <SECRET KEY>  -o

sls deploy
OR
npx sls deploy

```

### Enjoy 
![image](https://user-images.githubusercontent.com/39345855/199551616-eaedf846-6f59-480d-8eaf-73eccb5bdab8.png)



### Reference 

* https://aws.amazon.com/premiumsupport/knowledge-center/glue-job-fail-retry-lambda-sns-alerts/
* https://aarfahrayees.medium.com/easy-way-for-setting-up-notification-for-aws-glue-jobs-that-failed-using-sns-a002a52a1b72

