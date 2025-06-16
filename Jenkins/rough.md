- by default jenkins path is /var/lib/jenkins
- Here there are its files lets see job and workspace
- job contains jenkins created job configuration files
- where as workspace contains if we pull from git those files are stored in the workspace
- we can pull repo using scm or execute shell command git clone difference is in workspace/ scm directly installs repo files where as git clone installs the folder and inside it has its files
- While executing commands through shell in jenkins job it will be executed as jenkins user
- Build periodically - it is  a cron job triggers, build everytime even though there is no change in git
- poll Scm - build everytime, when there is a change (same cron task for timer) but only triggers when there is a change in git
- webhook - it only triggers when a commit happens
    - Enable GitHub hook trigger for GITScm polling in jenkins
    - go to your github repo settings (repo settings not main settings) there in webhooks add webhook and in place of jenkins url add jenkins-url/github-webhook under it select json format and save
    - now each time a commit happens it triggers the job
- In build we write what are the actions to perform
- whereas in postbuild seaction we write what are the actions to be performed after the build is done like sending an email or creating an archieve file so and so
- Instead of shell we can directly execute maven
- And to speciy which version to use go to tools in manage jenkins there if you have maven installed in your system give it's home_path and if you want a particular version check install automatically and select the version
- if we install new versions through tools then these packages are saved under /var/lib/jenkins/tools
- For private repostiories u can add credentials in the crendetials section in manage genkins select type of authentication if username and passwd the passwd can be of PAT and ID is simply the name of that credentials if we don't mention that it is generated ramdomly
- Jenkins have something called master and slave(worker nodes) architecture
  - Where instead of running all jobs under a single machine we can configure them to run on different marchines based up on our requirement
  - In it there are two types static and dynamic slave
  - static slaves are like single machine that we create for our task and even if the task is done the machine exists
  - where as dynamic slaves while we create a a build tast it creates a container whenever job is done it is deleted
  - In order to mention what job to run in which node we use labels for that
  - For this creation go to Nodes in the manage settings click on add nodes
      - and the no.of executors mean how many tasks that node must run if it is 2 then two build tasks will run and 3 one will be in the queue
      - if you click build 2 times for the same task the only one time it will start even the executors are 2 the second build of same job will be in queue
      - If you need to run multiple jobs then in job configuration enable "Execute concurrent builds if necessary"
- If we want to maintain interconnectivity between jobs i.e, for example if build job is success then that should automatically trigger the sonar job and if it is success then it must trigger docker build and pust and so on
- If we want to maintain this type then there is a concept known as downstream jobs and upstream jobs
- This is a leagacy way which means if we are still using free style jobs and folders then we use this way
- We can create a folder and mention some jobs there and make sure that particular developers are having access to only those folder (i.e, only jobs inside that folder)
- Simply we can group multiple jobs in a folder
- If build 1 is triggering build 2 then for build 2 build 1 is upstream and build 1 build 2 is downstream
- For this in folder after creating new item you need to select post build action  Build other projects  and select which job to trigger
  ![image](https://github.com/user-attachments/assets/203d5242-80c9-4d1a-8339-9c1bc2191f32)



