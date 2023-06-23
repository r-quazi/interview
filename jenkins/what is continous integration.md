# what is continous integration ?

Ans : 

Continous integration is a process where build ,  test , storing artifact happens.

lets take an example , once the devloper commits from laptop and push to github , the github will send http post to jenkins if we configure the jenkins webhook in github , because of this the pipeline or job will trigger in jenkins.

the pipeline can be divided in 2 steps CI and CD ,

In CI we can have multiple steps first we will fetch the code , will build the artifact using gradle / apache ant /maven for java based application and npm for node app.

after build we can test the application using plugins or by a seperate server , jenkins provide unit testing -- we need to install junit plugin for this , we can test using the sonarqube and can apply quality gates to ensure we get the output required as per company policy and our artifact should meet the code best practices.
we can test using scripts aswell. and testing like smoke testing , unit testing , also we can run test in different browser , we can add steps in jenkins file to run the test in different docker container eg docker container running chrome , next firefox, edge , safari etc.

or we can run on different OS as windows , linux , etc


since this will become long running each test on a platform which will increase the time , jenkins provides a good workaround by running jobs / steps in paralle.

when running jobs in parallel we need to make sure node is available at the moment and executer is available.


once the artifact is built and tested we can archive the artifact or we can store in nexus repo or any other platform like jfrog or , S3 , github artifact repo etc. It is a best practice to enable the fingerprint this will tag each articact generate a unique hash number so that we can find which was stable artifact and in which artifact we fixed the bug, 

also this will be helpful in upstream / downstream jobs to find which one using whcih artifact , jenkins does not store the whole artifact with a new name , it will just update the database i.e md5 checksum , this  helps in lesser use of memory.

next we can make an image with dependencies using docker and can update to dockerhub / nexus repo / jfrog etc. we need to make sure when making an image docker is installed in the system and up and running,  and a docker file is available or we can provide steps in jenkinsfile but as for a code reuability and versioning we should create a dockerfile instead of adding all the steps in jenkinafile to create an image.


also when creating dockerfile we should follow best practices and try to use less number of layers so the image size can be reduced and use a correct image rather than installing every dependency in a xyz image.


once the image is created and uploaded we can deploy and that will be a part of CD.
