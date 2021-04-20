# Jenkins Jobs Installation for Boomi CI/CD

This repository has the Jenkins Jobs required to launch Boomi CI/CD reference implemetation. The Jobs must be installed/copied into a working Jenkins installer 2.x or higher. 
  
## Pre-requistes
Must need administration access on Jenkins server and accesss to the Jenkins file system to install the jobs. This version only works on a Unix/Linux implementation of Jenkins. 

  - Install the CLI utility and its pre-requisites in the Jenkins server from [here](https://github.com/OfficialBoomi/boomicicd-cli)
  - Install the following Jenkins plugins required for Boomi CI/CD
      - cloudbees-folder
      - folder-properties
      - purge-job-history 
      - build-publisher 
      - htmlpublisher 
      - build-user-vars-plugin
      - secure-requester-whitelist
   - Copy the Account_{Rename} folder under the ${JEN1KINS_HOME}/jobs directory on the Jenkins server
   - Manage Jenkins-> Configure System -> Go to jenkins-url/configure and set the Shell Executable
      - Scroll down to Shell
      - **Shell executable:** /bin/bash
    - Manage Jenkins-> Configure Global Security ->
      -  Scroll down to Authorize JSONP or primitive XPath requests by whitelist
      -  Check the box "Allow requests without Referer"

Restart Jenkins after copying the folder.

# Configuring Boomi Account 

Configure Jenkins to connect to Boomi Account. (This assume firewall/proxy b/w Jenkins and Boomi AtomSphere is set). There are two GIT repos that can be configured (both optional). One is the Git Component Repo where the component XMLs will be automatically stored. The other the GIT Release Repo where the Boomi components can be deployed using a release template. [Examples](https://github.com/OfficialBoomi/boomicicd-cli/tree/master/cli/scripts/templates/configurations)
* Login to Jenkins and select the Account {Rename} folder & click configure. Review and update all the fields as required.
* Update the Display Name
* Update the the folder properties Name: accountId Value: <>
* Update the the folder properties Name: SCRIPTS_HOME Value: <Full path of CLI /scripts folder>
* Update the the folder properties Name: SONAR_HOME Value: <Full path of CLI / sonar-scanner folder>
* Update the the folder properties Name: LOCAL_ATOM_INSTALL_DIR Value: <ATOM_INSTALL_DIR on Jenkins>
* Update the the folder properties Name: gitComponentRepoURL Value: <GIT Repo URL if using GIT>. If GIT requires credentials use a secretText below
* Update the the folder properties Name: gitComponentRepoName Value: <Top level name of the GIT Repo; usually the part before .git>
* Update the the folder properties Name: gitComponentOption Value: <CLONE| TAG> if you use CLONE it clones the repo and pushes the content. Else creates a release tag (zip)
* Update the the folder properties Name: gitComponentUserName Value: <git --config global.username>. 
* Update the the folder properties Name: gitComponentUserEmail Value: <git --config global.email>. 
* Update the the folder properties Name: gitReleaseRepoAPIURL Value: The API URI for the gitReleaseRepo
* Update the the folder properties Name: sonarHostURL Value: <GIT Repo URL if using GIT>. 
* Update the the folder properties Name: sonarProjectKey Value: <Name of SonarProject (if using Sonar)>

# Configure secrets
* Select the Credentials menu from the left
* Update the authToken to the Boomi API Token (Format) *BOOMI_TOKEN.user@company.com:bOomi-aPi-ToKen-*
* Update the sonarToken
* Update the gitComponentRepoURL. If the gitComponentRepo has username and password
* Update the gitReleaseRepoUserPassword. To connect to gitReleaseRepo to recieve WebHooks. [See](https://docs.github.com/en/developers/webhooks-and-events/webhooks) 
* Update the gitReleaseRepoAPIToken. To connect gitReleaseRepo to update the commit status using an username and API token.
* Update the JENKINS_TOKEN. This is used to trigger Jobs using Jenkins API from DynamicGitJob jobs. [See](https://www.decodingdevops.com/jenkins-authentication-token-jenkins-rest-api/)
* Click Rename and rename the folder name to Account_YOUR ACCOUNT

## Run your first Job
* Click on the Account folder, select the the Publish Reports tab 
* Click on List Atoms Job
* And click on Build Now
* Once the build is compelete open refresh the output and select the html report

## Run Jobs
To run any of the Jobs listed below:
- Click on the appropriate tab/job name
- Select "Build with Parameters"
- Pass the required parameters and click Build
- Review the console output or Jenkins run output for success/error notifications

## List of Jobs
|Job Name| Notes|
|------|-----|
|Change All Listener Status| Changes all the Listener Status on a given Atom |
|Change Listener Status| Changes the Listener Status of a process on a given Atom |
|Continuous Package Deployment Pipeline| Executes a pipeline to create, deploy package, run separate Test process, validates process and promotes to another Env |
|Continuous Process Deployment Pipeline| Executes a pipeline to deploy a process, run separate Test process, validates process and promotes to another Env |
|Create Cloud Atom| Creates a Cloud Atom in a given Cloud |
|Create Environment| Creates an Environment in an Account |
|Create Environment and Attach Atom| Creates Environment and attaches an Atom |
|Create Packages| Creates Package Deployment for a single packages using processName or componentId. Alt will publish a report to GIT and integrate with SonarQube |
|Create Packages| Creates Package Deployment for multiple packages using processNames or componentIds. Alt will publish a report to GIT and integrate with SonarQube |
|Create Process Schedule|Creates Basic Process Schedule. For Advance schedules pleas use the AtomSphere UI|
|Delete Atom and Env| Delete Atom and Attached Environment  |
|Delete Local Atom| Deletes Local Atom (Local deployed on Jenkins) |
|Deploy Local Process and Publish to GIT| Deploy a process to Local Atom and extract the component XML to GIT (Legacy Deployment) |
|Deploy Multiple Processes| Deploy multiple-processes to an Environment (Legacy)|
|Deploy Package| Creates and Deploy a single package using componentId or processName to an Environment. Alt will publish a report to GIT and integrate with SonarQube |
|Deploy Packages| Creates and Deploys multiple-packages using componentIds or processNames to an Environment. Alt will publish a report to GIT and integrate with SonarQube |
|DynamicGitJob_Dev|This is the job points to the specific "Development" git branch. See notes below|
|DynamicGitJob_Test|This is the job points to the specific "Test" git branch. See notes below|
|Execute Process| Executes a process on a given Atom |
|Get Installer Token| Get a InstallerToken |
|Get Cloud Installer Token| Get a InstallerToken for a Cloud Molecule. Must pass the cloudId|
|Install Local Atom| Install an Atom local to Jenkins |
|List All Environments| Publishes a report of all Environments |
|List Atoms| Publishes a report of all Atoms |
|List Deployed Packages| Publishes a report of Deployed Components in an Env |
|List Package Components| Publishes a report of all Packaged Components of a given Version |
|List Processes| Publishes a report of all Process |
|Promote Multiple Processes| Promotes Multiple Process from one Env to another (Legacy)  |
|Promote Process| Promotes a single Process from one Env to Another |
|Publish Package to GIT and Sonar| Publish a package to GIT and perform Sonar validation |
|Publish Packages to GIT| Publish a package to GIT and perform GIT |
|Query Atom| Query status of a single atom |
|Query Execution Record| Query the status of a Process Execution Record within a given timespan |
|Start Local Atom | Start Local Atom | 
|Stop Local Atom |Stop Local Atom |
|Undeploy Package | Undeploy a Package component |
|Undeploy Process | Undeploy a Process (Legacy) |
|Update Environment Extensions | Use the JSON file created in the Create Package process to update envirnoment extensions. Use valueFrom to replace secret value with Variables|
|Update Process Schedule Status |Update Process Schedule Status of a single process |
|Update Shared Server |Update shared webserver details of a given Atom |

# Configuring Another Boomi Account on the same Jenkins
You can clone the existing Boomi Folder and change the required Account properties to configure a new Account for Boomi CI/CD on the same Jenkins folder.
Note: If the Build or Build with parameter menu is not available. Then disable the job and Enable this. Or restart the Jenkins.

# DynamicGitJob
* This is the job points to the specific "Development" git branch. 
* For multiple builds pointing to Test, PROD this job must be cloned and the "Branches to build" and "JOB_ENV" properties must be updated accordingly.
* GIT adminstrators must ensure controls to limit access to non-development GIT branches. 
* [Here](https://medium.com/faun/triggering-jenkins-build-on-push-using-github-webhooks-52d4361542d4) is a link to set up GIT & Jenkins to trigger Jenkins Build from GIT
* Click Configure and update 
* Source Code Management - [Enter GIT Release Repo Here]
* Credentials - Ensure the correct value is selected
* Branches to build - This has to be set to the dev/* branch
* In the build tab update. Note these properties can be set at the folder level or removed. If the JENKINS_URL is set. 
* export JENKINS_URL="http://localhost:8080/"
* export JOB_URL_BASE="http://localhost:8080/job/Account_Boomi"
* export JENKINS_USER="admin"
* Update the property export JOB_ENV="Development" to point to the Boomi Development environment. 
* This is to ensure the json configuration matches the target environment and prevent a Development config/job/git repo run jobs targetted to a non-development environment.
* Jenkins job can send a status update back to GIT as part of the Post Build Step. For set up [here](https://medium.com/@applitools/how-to-update-jenkins-build-status-in-github-pull-requests-step-by-step-tutorial-bf213a2eacbe). This has to be done for all relevent Jenkins jobs like Deploy Packages, Deploy Package, Update Extensions, Create Process Schedules

# Support
This image is not supported at this time. Please leave your comments at https://community.boomi.com/s/group/0F91W0000008r5WSAQ/devops-boomi
