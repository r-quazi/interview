# Which tool have you used to implement CI/CD ?
Ans : 
I have used Jenkins to implement cicd , jenkins is an open source automation server which allows us automate various stage of SDLC include building testing and deploying application, As per the forbes multiple organizations reported they delivery speed is increased by 40% after automating using jenikins or other tools like jenkins like travis CI ,circle ci, teamcity etc , the choice of tool depends on the specific requirement and preference of dev team or the organization.

jenkins is widely used also supports lot of plugins and itegration with other devops tools making it highly flexible and customizablefor example we   can configure user with Microsoft AD for RBAC for jenkins users.

jenkins supports multiple job styles it can be freestyle job , multibranch pipeline ,  supports organizational folder and unix directory struvture as well which makes it easier to seperate jobs / pipelines and environment. as jenkins integrates with multiple environmnets we can configure it with sonarqube / nexus / docker / k8  for cicd and for notifaction and incident management we have slack / email and pagetduty respectively. 

in pipeline we can can configure to run a job in specific controller , jenkins recommend to use master - slave as a best practice we should deploy master with multiple nodes /slave machine,  also we need to make sure master node is highly availabe and and should not be a single point of fialure.
