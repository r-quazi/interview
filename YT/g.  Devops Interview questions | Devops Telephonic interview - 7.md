##  Devops Interview questions | Devops Telephonic interview - 7 
https://www.youtube.com/watch?v=ndhcVCJ21IQ&list=PLLYW3zEOaqlLShAk9pd4FQ34KOpY7EJAq&index=7

------------------------------------------------------------



0:00
hello yeah yeah over here yeah yeah yeah can you please walk through like what
0:06
kind of experience of experience what kind of roles and responsibilities ah yeah yeah so I'll be in how into IT
0:14
industry so since five years and so in the hope so I'm working from last four
0:20
years and I worked in couple of tools like Jenkins mavin and
0:26
ansible and in few of the projects like we're in we wanted to do automation for
0:34
the manual activities so I worked on shell scripting and the containerization
0:39
tool like darker and kubernetes and artifactory I've used a frog and Nexus
0:47
so and also for monitoring I've used of Prometheus and Griffin and other
0:54
supporting tools like migrant and those kind of things have used these are all
0:59
the tools that are from was then how many years of experience you are having total total is Phi so relevant like in
How many years of experience
1:08
DevOps oh it is for to have a cloud exposure like any cloud experience into
1:14
something like Microsoft Azure yeah II WS I have experience but yeah it was
1:21
kind of like piwo see I mean like we wanted to implement the EWS so we just
1:27
used Seraphim and so then be used to create individual services but project
1:33
experience though I mean it's it's not that much in AWS cloud cloud things
1:39
that's fine but you know the basics are basic detailed basic information of all this yes yes yeah yeah
1:45
yes once you get a chance maybe you can explore on to this services and you can
1:51
try to finish the task right yes yes let me come to this integration to contains
Integration
2:01
delivery okay so you said like you have work done couple of tools yeah like we haven't really get a big bucket another
2:08
yes yes so before jumping into Marvin or something let's first understand like how the
2:16
determined overly come get a processor what is a branching strategy or following it and when we during
2:23
production so how are you going to handle it for merging requests from Shawn's own
2:30
branch to source on branch so you want to know the process of yeah so I mean it
2:38
depends on the project so because I've involved in multiple projects right so in one of the project it was um what
2:46
used to they used to do is like master branch is a stable one and so they'll be
2:51
having one more dollar branch so from dollar branch so every developer who
2:56
ever wants to contribute to that particular project so they will gonna create a feature branch and then so
3:03
we'll so what they'll do they'll create a feature branch and then they'll write their code and then after that like
3:10
they'll gonna push it back to the repository and then they'll raise a PR or to merge it back to develop so in
3:17
this PR so you should add like reviewers like your manager sort of see the
3:23
question here during production right the code is like base code whatever the
3:31
latest code which is into production like before going to production like pre prod so your code is merge two root two
3:38
something some that there should be some branches right like maintenance branch or something you must be having the
3:44
branching yeah yeah so I mean out from developer master so they'll go and
3:50
create a release branch so from the release branch the it will go to production okay okay so it will be
Merge branch
3:57
merged after the once it is going to the production and successfully merge so you
4:03
are going to merge it yeah once the merge is done like successfully that is Mars is done so that feature branch to
4:09
develop era master so then so I mean we in our projects like we had some
4:14
timeline so every month or every 15 days we wanted to give a release so that time so the leaves branch will be created and
4:22
even the tax will be created so for that particular branch and major release our like minor release or
4:29
something kinda I do be release is a major major version so we're in now we
4:34
have another branch which is hotfix so we're in like it'll be like small production changes if it is simple
4:41
changes you know so they used to do that and when we release or fixes those so then that'll be our minor versions
BPAs
4:49
perfect so coming to this aap is have you heard about to get her BPA's yes yes
4:56
so I have told you right like have worked in many automation things you know so one of the I mean requirement
5:04
for us was like how we wanted to identify we had almost like 200 to 300
5:09
repose so we wanted to identify which branches are inactive means like since two months so what are all the branches
5:16
they have not updated so that we considered it as like inactive so and
5:21
then now so we wanted to identify those things so the major issue was like few
5:26
was therapist had like more than 200 branches so using doing it manually it
5:31
was very difficult actually so that's the reason so we used to like use the
5:37
eps and then we used to get the branches and all so that that we used to do so on
5:45
a lot of other things as like not only that branches a lot of other things we used to do like obvious EAP a you have
5:53
looked on it together it is a bit bucket EAP or like eater BPA yes bit bucket and
5:59
get a both have work done so can you
CPA
6:06
tell me one thing about like how you can reach out the repository is based on the
6:12
CPA what is the structure going to follow yeah so first we need to have
6:17
that term I mean our internal servers I mean whatever the addresses and then we
6:24
need to have slash the best EPL slash you need to maybe like I don't exactly
6:30
remember that then you need to have summit indication so not a tent occasion you need to give repose and so
6:38
and the rest /ap a slice repose many do that like I kill gonna list out all the
6:44
reposing that particular under that particular username so you need to supply like eyghon you use a name and :
6:52
password you need to supply so for that particular report I mean that particular user what are all the reports are there
6:58
I click on a list perfect so when it
Webhook
7:04
comes to web hooks right so when I have evil done that folks like what is the
7:11
basic idea of anything yeah so if any event happens like in YouTube or github
7:17
bitbucket like let's say some commits has happened or somebody some deleted
7:23
some branches so any activity that happens in github so if you want to report it to any tools like jenkins or
7:31
anywhere like so that time you can definitely use where books and so if you're going to inform that particular
7:37
system so what has happened so for that down I mean reason we will use Web books
Configure
7:46
one thing you see when you try to add this configuration straight or get
7:52
configure and so you go in to set the first initially the username under which
7:58
file you were going to edit it in that case I don't remember but by using
8:03
command actually get conflict dot email you can give set it but I don't remember
8:09
the file exactly but I guess so when you install gate so there will be a folder
8:15
which is created get underscore score so like that like under that folder so
8:21
maybe we have a global config file server and we will set all those things
Dependencies
8:30
done this Marvin or cradle which are
8:35
yeah I'm comfortable with Navin okay perfect can you tell me that like boom
8:41
dot XML which it has some structures right like when it comes to build and
8:47
for dependents is yeah let's say I have some next dependency okay what is this like how
8:54
are you going to pick the structure and where you are going to pick the structure along you to go along with the
8:59
ocean what are the syntax yeah so I mean if you want to create any project like
9:06
in mavin so you need to definitely have humming pounded XML in that mandatory
9:11
fields are unity have like the initial talk tag that XML time and after that
9:18
you need to have GA base group ID artifact ID and version and it depends on project what you are da looking like
9:25
if you want to have a dependency is there plugins so depending on your requirement you can search like I mean
9:32
are in the mavin documentation itself so there will be a no I mean central repository later they have a good
9:38
documentation so where you will go and you will fetch the group ID artifact in versions of that dependency and you'll
9:45
define it under your dependency type so if it is a plug-in so it will define it under plugins and there are many other
9:51
fields like packaging is there and so you can have a mail list and
9:58
distribution management so there are a couple of fields that you can use it I
Uploading dependencies
10:04
have one question here let's say I have a couple of dependencies lately let's
10:10
say I have a bulk of dependences okay about 30 to 40 dependencies okay I want
10:16
to upload them to the Nexus okay okay so this dependence is I want uploaded and
10:24
make sure that I do not have internet connection in my build server okay okay so I have to do it a manual so you know
10:34
the command to which command is going to use the dependencies in oh you mean
10:42
deploy I mean I don't know I'm confused bit so I'm thinking like so by using
10:48
ambient deploy so wherein you can upload whatever the artifact has been generated
10:53
by particular project here is a possible to upload the ambient deploy you have to
11:00
do each of your iteration right one yeah one after each other and format racketing format let's say you
11:07
have something related to go automation to pipeline like in some young you want
11:14
to send it right this should be some structure my comrade Ward something Apache yeah so every time you have to
11:21
give maybe I'm a vent deploy and then package name and whatever it is whether
11:26
it is a jar file or pom file distribution files yeah so can we do it
11:33
through script and together and send it may be possible but I'm not sure about
11:40
that like how we can do it maybe some options definitely will be there with a novel but I don't know about that okay
11:46
okay that's fine that's fine okay can you tell me the life cycle of lovin yeah
Life cycle
11:53
so life cycle there are like three build stage build life cycles when it's a
11:59
clean default and site so in default we have seven stages so we're in now the
12:05
first one is verify so verify is just verify so whether whatever the given information is proper and the syntax of
12:12
the form not xml is proper or not and then we have now so after that we have
12:19
compiled so it will compile your code it is gonna create dot class files so for
12:25
you intermediate class files and then we have tests so when it will create it'll
12:31
apply the test cases unit test cases on your created dot class files and then we
12:37
have a pack easy package so it will create the artifact for us and then we
12:42
have verify so verify is for applying the integration test cases on created rural warfare and then we have install
12:49
and deploy install is for like local installation so there is something called as dot m2 folder so which is all
12:56
this Marvin's local repository when we will push a little copy the war file to
13:01
that particular place and MA and deploy will like used for deploying the jar file war file to a repository
13:10
private repository okay I have one use case in Jenkins let's say
Copy Jenkins
13:17
can you tell me the process how we can move our copy Jenkins from one server to another
13:22
server oh yeah so we can basically we can copy dot Jenkins of a folder or from
13:31
one server to another server and then we can start these engines there with the same configuration so with the same job
13:37
everything like plugins configurations everything so if you want specific job so you can use there are a couple of
13:44
plug-ins for that are else like you can manually go to tour Jenkins folder and you can take you need to go for jobs
13:52
folder and under that job folder so for each job we'll have a config dot XML you
13:57
can copy that and we can paste it wherever you need and then you can in that server you need to go to management
14:03
keynes and reload from disk unity to do so that that job will be displayed on
14:09
using kids okay okay comes to plugins right or in any case so can you explain
Plugins
14:15
me about there are few important roles and like plugins angelicus yeah so
14:22
whenever like see at the okay you want to write it pipeline there should be
14:27
some prerequisites and if you how to download the plugins and in order to
14:32
proceed the pipeline to it yeah yeah that's so if you want to write pipelines so you need to have a pipeline plugin so
14:39
that has to be installed and as obviously you might so use many tools
14:45
like Marvin or it can be Gretel anything so related plugins you definitely need
14:50
to use like docker and all like the gradall maven plugins you should install before using it and yeah so I mean like
14:58
we're at the time of installation it will give a suggestion like install all the suggested plugins so any click on
15:04
that the basic plugins will be installed but if you want in case like you can go to manage plugins and then you can
15:11
install whichever you need okay okay when it comes to these parallel

Parallel Execution
15:16
equations right number of jobs yeah you can set a threshold value threshold
15:21
limit in Jenkins right where you can do that configuration so we will be having
15:27
an option I guess the parallel execution itself so we're in
15:32
the first general section itself and you can specify number of threads like executors like so when in whatever the
15:40
number you give so it will be executed so I do you mean like the job should be
15:46
executed thoroughly or like let's say singles or based on your hardware based
15:51
on your requirements there should be a sum only the limiter only you can run parallel 3-4 jobs
15:5
let's say you got any requirement that will be how to run parallel e at least
16:04
of 210 jobs in 30 how to procure like you how to at request then to increase
16:11
the memory and these things yes also handle it you know that increasing like number of executors yeah and we can set
16:18
the executors like will have a section where in we can set in a master itself
16:24
we can set executed a number of executors yeah we can do that here in
16:29
your build server do you have a master slave concept yes we have ok how many
16:36
slave missions are there play machines it is like six machines and so I mean
16:44
like master and we have sleeves so to distribute the load and also we are
16:50
making sure like all the applications has a docker in it because we are using
16:55
a node as a docket so that like if something is missing so I mean so we
17:01
don't need to install mavin and gradall explicitly so when we have a docker so we can specify the image and we can run
17:08
on that a couple here later when it comes to agile methodologies people say
Agile methodology
17:14
people talk about into more integer a jail the methodology and this is right yeah
17:19
what is the main difference between a jail methodology and SDLC so SDLC is I
17:25
mean like we're in once you take the requirement so maybe it freezes like it
17:33
freezes like you you will work on it and then do the product to the customer then
17:38
in agile so it has some sprints and so what I mean depending on the requirement
17:44
like you your if a customer needs a very important feature to be implemented but
17:50
you are working on something so if that is so important then you can jump on to that task and then you can come back and
17:57
you can work on that so this is a Jile like the customer I mean whatever II used
18:02
like the importance will be there and for each and every task there is there will be a specific term which is
18:08
assigned but we're in sdlc so we'll take a bulk requirement until unless that is finished you won't take anything so
18:15
you're in agile you are giving down credibility to the customer when we can
18:20
give the changes and so we can work on it so so I mean you can take a new features
18:26
and you can implement it so that's that kind of thing okay okay
Nexus
18:31
coming to Nexus so you said like you worked on it Nexus right yeah yeah so Nexus what are what are the activities
18:40
you are going to perform in the Nexus so like let's say some xox person I like
18:48
let's say developers want to move the the distribution is like mapping distributions
18:53
I mean be a model to distribution in that case how are you going to ask you
18:59
the access to them mmm in pod sorry I am NOT work then so my part was like just
19:04
creating a repository and configuring it and like having those kind of stuff so
19:09
administrations no no I have not worked okay perfect noches so you you worked on
19:17
events on octave also right yes yes yeah okay so what is the difference between sonar quality created quality profile so
19:26
quality profile is basically I mean now you will define like what what is the
19:33
condition means like how you are profile in the sense it's kind of a rule in a
19:39
layman term 600 L it's a rule so we're in like quality gates is like you are putting some condition so you need to
19:46
meet these conditions and then then only you can proceed so profile is like something rule you're creating like so
19:53
for example like if a customer as a requirement at the class means start with capital letter and end with
20:00
capillary capital letter so then you can create some rules profiles like us on
20:08
our profiles and rules so we're in quality gate it was like your ex are you
20:14
are telling that like if firing a five classes which doesn't have these conditions it's fine if it is classes
20:20
more than five and then you need to make sure it is fins this so not Q right so
20:33
as soon as you go to likely let's say first you're going to do the so that's konasana scan and then and when it comes
20:40
when you as soon as your quality condition is not it is not going to make
20:45
the condition obviously you have to fill the job right yeah that dot activity
20:51
area where are you going to specify in the build as part of Belgium yeah so we
20:56
have integrated sonar with Marvin itself so we will do em in so before like once
21:01
the code is check out the next step we will use is ambient sonar sooner okay so what it does it will communicate
21:08
with the sonar cube and then so it will just like check the quality gate so in
21:13
that we will have a black block wherein like quality Gators okay or not so we
21:19
will have we have a class wearing like it gives returns like whether the quality jet is success or not so I mean
21:25
once that that isn't so it is just check for the quality gate so we will get some response so if it is are true so then
21:33
like then proceed or else like then feel and if you if we have configured any
21:39
mailing things and like in the post block so then we can we will do that so
21:44
yeah the first step will be that once the check all tasted okay how you work
21:50
their hands it will oh yeah oh yeah yes I got them let's say I want to see the
21:56
list of like how many ansible variables are available so how can you list out
22:02
that how do you see the list of variables variables no not sure about it
22:09
okay please protect the connectivity between your hosts like which command are you
22:17
going to use it we can use set up module and ping module so - just to check like whether the connection is there or not
Playbooks
22:24
okay so as part of this automation process plate automation activity start you might have written some playbooks
22:30
mmhmm yeah kinda play books it was and so what it is got benefited the customer
22:36
based on your automation effort so basically we have used we're in a place
22:42
like we wanted to integrate help and then so now docker so there we we used
22:51
to use ansible ok so there I specify I mean we have used ansible so what what
22:58
it does is like so we will give a docker image as an input and also a he'll in
23:03
charge first input so ansible the first thing is according to the environment we
23:09
used to take a particular values so that is stored in the ansible playbooks
23:14
itself so in some of the folders I'll apply those things onto the help charts
23:20
and render it and then deploy it onto kubernetes cluster so there we have used and for the small terms like copying
23:28
from artifacts from the Jenkins server to the destination so there was QA
23:33
service those kind of stuff really update and also you know so in our
23:39
project like we wanted to do a couple of like automation like if a new person
23:44
comes so so rather than doing the setup manually so we wrote a ansible playbook
23:51
if they run that playbook so all the setup will be done so we have avoided
23:57
much wastage of set-up time ok this models where you can pull out lists of
Models
24:04
module tangible modules we have a good documentation like ansible dogs so we
24:11
can we have all the modules information about that so we can we can just get
24:17
whatever like the modules that we need so when it comes to container
Virtualization
24:24
Jason trained advantage is that container Cantara Gatien provides the or the
24:30
virtualization concept containerization is basically I mean a virtualization has
24:36
few disadvantages like so when you install a virtual machine on top of one
24:42
oh s so basically virtual machine will also have OS so whenever the main
24:49
machine goes off so it will take my let's say it will take one minute to come up okay so and to come up virtual
24:56
machine also it will take one more minute because there are two different voices okay so the some of that is two
Containerization
25:02
minutes where an in containerization so the containers do not have its own voice so it will use the voice which is
25:09
underlined in the installed machine okay so so here in this case like it
25:15
the uptime LaCava the off time for the machine will be only the underlying
25:22
voice so it doesn't know the time required for in virtualization for the
25:29
virtual machine is not required here so that like that even one minute M a one minute matters and resulting projects
25:35
that is one thing and virtual machine images are very highly where I mean like if you want to install it like it'll be
25:41
the final configuration files itself it will be like more than 2 GB 3 GB files so when I mean containerization it's
25:48
very lightweight and that is one more advantage and so other things like yeah
25:56
memory waste is we can avoid that as well so once if you allocate like 4gb
26:01
for a virtual machine so you can't take it back from that virtual machine ok perfect
Container Edge
26:06
I have one question here when as soon as you were docker container edge it's
26:13
right or am I going to like lost the day long am I going to lose my data or
26:19
something like what will happen when a as well as container it yes so if you don't have volumes
26:24
attached to your container so did indefinitely or the data or which you have in container will be lost so that's
26:31
a like if it is persistent application so then you should attach a volume or a mounting so that like even container
26:37
exits so you'll have the data and you can attach it back whenever you're you create a new
26:42
container or whenever it comes back okay well it's basically what is the meaning of darkest one and what Gandalf will
26:51
like how are you going to declare your like applications of whatever it may be
26:58
like to try it on sweetie replication so what what is it basically to talk alpha our darkest one is basically the
27:04
configuring because see containers will create an emission okay so you need to have some like management over your
27:12
missions as well because if you keep on create a containers on one machine so definitely gonna like I mean even that
27:19
has a memory so it will be in a it will be gonna be consumed and so it won't be able to take any more load so to Andal
27:27
those things and basically managing the nodes and the containers so where it should go
27:32
so which node is perfect for that particular container so this kind of management we will go for Dockers form
27:38
so which is if you want to say like it is similar to cuban it is where in so it
27:43
will manages the node and it tells like where the container should be created and what memory should be assigned and
27:49
so those kind of stuffs right will give you now specified this your activity as
27:57
part of your current project right yeah you said like you work done involved you've done like uber it is creating
28:04
quality subjects yeah like deployment service and service accounts yeah
28:10
can you explain about detailed information like what is a what is this
28:16
cooperative object and very varies this ingress is used and what kind of service
28:21
you have used it for deployments so yeah so if you want to take an application so
28:27
it is not only are the deployment so deployment is actually a small part so
28:33
supporting to that there are many things like deployment is like just you're creating a deployment of your
28:38
application and to be accessed from the outside world so you should create a service ingress ok services basically
28:46
there are a couple of types like cluster IP node IP so node port something like
28:51
that so closer IP so if you want to access your application inside your cluster itself inside your to be needies network
28:57
so then you can go for that if somebody wants to access that a particular
29:03
application from outside world so then you need to go for node port and then with that like we have on many other
29:08
objects like config mohab set of secrets so if you want to copy any configuration from look file from your local on to
29:16
parts then we can use conflict maps and if you want to create any key value pairs in a ramen trailer bus or
29:22
something like that you can use config maps at that time as well and ingress coming to ingress so it
29:29
is basically I mean so if we you should have one single service single application so then you don't need to go
29:35
for that so if you have a couple of many applications that is deployed on your
29:42
cluster so then you can go for it so we're in it gives a come in good
29:47
security and also like with the same address like so if you want to tell in a
29:54
common way so like let's say we have a Facebook okay so when we say Facebook
29:59
slash home so it goes to home page when you say Facebook / something like books
30:05
so it it might go to some books page so if you want to implement those kind of thing like you'll use the same address
30:11
but depending on the the last part like handler part so you need to redirect
30:16
your application to something else then you can go for ingress basically it is for routing and then we have a couple of
30:23
gigs like Network policies and yeah so yeah these are the things that have you
Zero Downtime Deployment
30:29
people talks about more into this zero downtime deployments right yeah so how
30:35
do you deploy the feature with a zero downtime in kubernetes so I mean so
30:40
deployment we can see we have something called as Linus and readiness probes and
30:45
so whenever the container goes replica set will take care of goettler I will
30:52
tell will be taken care about your pods like if it is down and question one quick question so a trainer up to you
30:57
yeah you're saying replica set right is a latest version able going to use the
31:03
replica set and preheat to ridiculous Ethel was there
31:08
any method instead of replicas it yeah replica controller was there so before replicas said it is replica
31:14
controller when you create a deployment so it actually creates a replica set and then it creates a pod zero downtime CR
31:25
so I mean replica set will be taking care so whenever your container goes off like if somebody manually deletes it so
31:33
it will make sure whatever the replicas that you county of given it will be always maintains that so let's say if
31:39
you have given three so it will always maintain three instances of your application and apart from that there is
31:45
something called as likeness and readiness proof so when you start your application so this means will this in
31:51
slightly over blip monitoring the pod right yes yes so we'll have some endpoint like hills
31:58
or something like so the configured endpoint so we can use that and then we
32:03
can more definitely we can monitor our containers whether it's performing well
32:10
you can use that like lioness hundred a nice pose what is the difference between
Replica vs Replicas
32:17
use it right before this replica satyr this replicas replica replication
32:23
controller yes it is a main difference between a replica controller and replicas it so in duplicate set so
32:32
whatever the containers like the labels you will have right so you'll specify that like so even it's like what what it
32:39
does like if let's say a plot is created already with the same label and you have specified three so what it does so it
32:47
checks like already one has been created so now it'll if you if your replicas is
32:52
three so then it will only create two so when I mean replicas a replication controller there is no such thing which
33:00
is called as match labels or something so that's right it will just create three instances for your application one
Rolling Update
33:09
question on rolling update as soon as you do the deployment like you are going
33:15
to use some rolling updates mechanism by it yes yeah so are these deployments like
33:20
if you are having more than one replica automatically doing ruling updates when
33:25
a new deployment config is applied okay so how it is this how it is being
33:33
processed when it comes to rolling update yeah our rolling update it's like
33:38
so let's say you have three instances of your application okay so when you do a new deployment new
33:45
new deployment you're creating so that time what it made sure is like it will make sure one instance is down and it'll
33:52
make sure one is up like it'll make one down and it makes sure another the new
33:58
instance is one new instance is up so then only it will make sure another
34:03
instance another application instance is done so if it fails then it will stop that decline process and to say directly
34:10
there is a some error so you have I mean the two world instances will be still
34:16
running but the third one it's already done so I mean with the new application
34:22
like one poor will be there with you so one by one to make sure one down and one
34:28
up when the new version comes up okay okay coming to this shell scripting how
Shell Scripting
34:36
we worked on shell scripting or portion its shell scripting okay what is this
34:42
error code when it comes to success you might be passing some male arguments
34:48
right yeah so I mean like EPA calls is something like that early there is
34:54
something called as exit status so which gives like if it is if your previous commander is like success so then it it
35:00
returns zero so when your previous comment comm whatever command is not
35:05
success then it is kind of like non zero value will get okay I have one question
35:11
key quick question here what is this dollar like at symbol or what what it is
35:16
going to do so dollar at symbol it gives us all the you know all the parameters
35:25
that you have sent from the command prompt like when you run your shell script right so
35:31
dot slash and special script name and then if you give the parameter so like
35:37
let's say your shell script accepts and parameters so then it prints or it prints all the parameters that you sent
35:43
from the command prompt okay I want to display like let's say I have a directory I want to only list out
35:51
directory contents again sub directories as well as list of files I want to
35:56
display only files list of files ok I want to exclude like this directories
36:03
and at least we can do yeah we can do
36:09
that so so by using there is a initial script there is - F thing so when you
36:17
give - F and the filename or directoryname if it is a file then it would be - so if it is not true so then
36:24
it is assumed to be some not file like it can be a directory or it can be something else so you can use hyphen F
36:31
and if you provide a file name you know if you you would need to look through each file and then you can do that and
36:38
maybe like in LS also there might be an option like - F or something like that but yeah if I am there like I know that
36:45
like there is option we can use iPhone F and the file name so which is said to be - if it is a fire
Pipelines
36:57
pipelines yes what kind of pipeline whether it is a declarative pipeline or
37:04
it's a declarative one okay so how are you going to put the stages how are you
37:10
going to write the stages and what is the process you have followed in your
37:15
project how it is got improved when it comes to deployment build using the
37:22
pipeline instead of manual build triggers and doing deployments oh yeah
37:28
so pipelines I mean we can integrate many things like so I mean you can
37:34
integrate the map into and then ansible so whatever the tools that you are dealing with you can do one after the
37:41
other so that is one advantage and also like cars Indians file it's a cool the Jenkins
37:48
configuration as a cold so I mean if someone doesn't have access to Jenkins so then they can say what configurations
37:55
has been done in the Jenkins by scene just like Jenkins file that is one like
38:02
advantage of Jenkins pipelines OKC let's
Sending an email alert
38:10
say as soon as my deployment is completed in in the last stage right I
38:15
want to send an email error to the saying this deployment is such as and so
38:21
on so on so on so artifact I have deployed to the end server target can
38:26
you really do it through the stage and like send an email alert and what are the prerequisites required as part of in
38:33
order to send an email alert to the development team or shown some teams yeah so post section we can use the post
38:41
section for that and like in the post section so we can use one more section which is called a success so if it is
38:48
success then like we'll configure so before that you should configure SMTP
38:53
server so your you will be you should have one of the smtp server that should
38:58
be configured in your jenkins so under configure system you need to configure that and then now some email lists like
39:06
you need to in the like post section so when you're using so you can so I mean
39:13
in pipelines we have a beautiful feature like we're in like so we can generate pipeline syntax so I used to use that
39:18
like so when you select are your mail configuration so it used to ask like who
39:23
is like a recipients so when you give that like you get a line from that snippet generator so it will just copy
39:30
paste my little text perfect one
39:41
question I want to remove the volumes I want to delete all the volumes on my
39:48
current host yeah
39:56
dr. vol prune or we can do that and we can do we can delete it do you have idea
Titan
40:07
about Titan no sorry I don't know I'm just more into cell scripting so
40:16
basically this when you sit like you have you have done zippy was he on AWS
40:22
right yeah what kind of like how what is the process if you want to give specific
40:29
roles and where are you going to do like bison granting the access to the zones
40:36
and person yeah we can use the I am service for that so we're in we can give
40:41
the access based on user like if they want only for programmatic access or if
40:49
they wanted only to access s3 bucket so then we can create a user and we can select the policies for that particular
40:56
user and you can you can give I mean like the credentials for it yeah we can
41:01
do that by using are you interested -
41:07
are you willing to work in nature instead of yeah yeah that's fine for me like it will be the same like all the
41:14
cloud I guess it'll be the same maybe only the wording says like the little concept might be change that's all I
41:19
guess are you willing to work any shift
Shifts
41:32
like this basically it's a UK project so you may have to work on AWS instead of
41:39
it Apple yes we may have to work on services there are few applications we
41:44
are we have we have hosted and we have roasted on your services so you have you
41:50
should get a knowledge before onboarding into our project I will try to give my feedback to a chair and do you have any
42:00
questions no I don't have anything because you mention like what work and
42:07
thank you thanks for your time thank you thank you for me
