# any alternate tool do you know for cicd ?

Ans : 
Yes , I have used the AWS Code pipeline which  is similar to jenkins used for build - test - deploy ,  AWS code pipeline is a PAAS Service they take care of backend things , since it is paas someone wo need system level acces is not possible and we cant configure like the open source jenkins we nned to use plugins / tool advised and supported by AWS Codepipeline , for example we need to use AWS SNS for notification . though we can use slack with aws codepipeline but the integration is not as smooth as jenkins , we need to create cloudwath event then  sns topic  then a lambda function  which triggers slack notification. 

so the choice of tool depends on dev or the organizations depending on their unique prefrence and requirements.


there are few other alternat tools available like travis ci , circle ci, teamcity , aws codepipeline etc.

however jenkins is widely used and support multiple devops tools / plugin which  makes it more configurable and customizeable as per the needs. 
also the community matteres whhile selecting a tool , lets suppose we are using a tool that does not provide support and even does not have community to get the answers if we got stuck at any point , this will be hard 
