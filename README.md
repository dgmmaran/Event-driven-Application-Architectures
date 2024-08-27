
# Building Event Driven Application Arhitecture




Overview

## Many customers are choosing to build event-driven application architectures – those in which subscriber or target services automatically perform work in response to events triggered by publisher or source services. This pattern can enable development teams to operate more independently so they can release new features faster, while also making their applications more scalable. In this workshop you’ll learn the basics of event-driven design, how to choose the right AWS service for the job, as well as how to optimize for both cost and performance. Through hands-on practice, this workshop will give you the skills to bring event-driven design patterns into your own applications.


## AWS Experience: Intermediate. Time to Complete: 2-4 hours. AWS Services: Amazon EventBridge, Amazon SNS, Amazon SQS, AWS Lambda, and more. Prerequisites: An AWS account and the latest version of Chrome or Firefox browser.






<img width="1792" alt="Screenshot 2023-02-08 at 08 03 15" src="https://user-images.githubusercontent.com/71371405/217471120-307547fd-3916-40a6-8036-63efee4ecd30.png">

- - Step 1 - - : 
- Create a custom event bus
Open the AWS Management Console for EventBridge  in a new tab or window, so you can keep this step-by-step guide open.

2) On the EventBridge homepage, under Events, select Event buses from the left navigation.
3) Click Create event bus.
4) Name the event bus Orders.

5)Leave Event archive and Schema discovery disabled, Resource-based policy blank.

6) Click Create.

Congrats, you should creat a bus, like underneath.

<img width="1792" alt="Screenshot 2023-02-08 at 08 03 15" src="https://user-images.githubusercontent.com/71371405/217474662-afd1d5d9-fe17-4231-ab40-1a40eb6d66e6.png">

- - Step 2 - - : 
Set up Amazon CloudWatch target (for development work)
Cloudwatch is great for monitoring, so when we set this as a target we can have rapid response for events. 

1) From the left-hand menu, select Rules.
2) From the Event bus dropdown, select the Orders event bus
3) Click Create rule 
4) Define rule detail:

Add OrdersDevRule as the Name of the rule
Add Catchall rule for development purposes for Description
Select Rule with an event pattern for the Rule type

click next

5) In the next step, Build event pattern
   under Event source, choose Other

![image](https://user-images.githubusercontent.com/71371405/217477511-14e99814-bcb7-4bf2-b603-147716fe1f59.png)

Under Event pattern, further down the screen, enter the following pattern to catch all events from com.aws.orders:

{
   "source": ["com.aws.orders"]
}

6) then select next

Select your rule target:
From the Target dropdown, select CloudWatch log group
Name your log group /aws/events/orders

7) Skip through the configure tags section, review your rule configuration and click Create.

- - Step 3 - -: Test your dev rule
Select the EventBridge tab in the Event Generator .

Make sure that the Event Generator is populated with the following (if you clicked the link above then you should see this pre-populated):

AWS Region should be to the region in which you are running the workshop
Event Bus selected to Orders
Source should be com.aws.orders
In the Detail Type add Order Notification
JSON payload for the Detail Template should be:

{
   "category": "lab-supplies",
   "value": 415,
   "location": "eu-west"
   
   Then click
   
} 
![image](https://user-images.githubusercontent.com/71371405/217493525-fa43acae-645a-4392-928f-60d200675f5c.png)

Open the AWS Management Console for CloudWatch  in a new tab or window, so you can keep this step-by-step guide open.

Choose Log groups in the left navigation and select the /aws/events/orders log group.
Select the Log stream.

![image](https://user-images.githubusercontent.com/71371405/217495960-caec45d5-4277-4f21-948f-4076eb451f13.png)

Toggle the log event to verify that you received the event.
![image](https://user-images.githubusercontent.com/71371405/217496184-f1adff43-aa86-4c5f-97f9-28b780cfb65b.png)

REMEBER - Eventbridge is great for so many different resources - want to track Lambda functions, you can! Timestamp an upload to an S3 bucket, easy!

NEXT - We'll target an API end point - a Lambda function - and SNS 


