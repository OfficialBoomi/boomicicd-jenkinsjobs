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
   - Copy the Account_{Rename} folder under the ${JEN1KINS_HOME}/jobs directory on the Jenkins server
   - Manage Jenkins-> Configure System -> Go to jenkins-url/configure and set the Shell Executable
      - Scroll down to Shell
      - **Shell executable:** /bin/bash

Restart Jenkins after copying the folder.

# Configuring Boomi Account 

Configure Jenkins to connect to Boomi Account. (This assume firewall/proxy b/w Jenkins and Boomi AtomSphere is set)
* Login to Jenkins and select the Account {Rename} folder & click configure. Review and update all the fields as required.
* Update the Display Name
* Update the the folder properties Name: accountId Value: <>
* Update the the folder properties Name: SCRIPTS_HOME Value: <Full path of CLI /scripts folder>
* Update the the folder properties Name: SONAR_HOME Value: <Full path of CLI / sonar-scanner folder>
* Update the the folder properties Name: LOCAL_ATOM_INSTALL_DIR Value: <ATOM_INSTALL_DIR on Jenkins>
* Update the the folder properties Name: gitRepoURL Value: <GIT Repo URL if using GIT>. If GIT requires credentials use a secretText below
* Update the the folder properties Name: gitUserName Value: <git --config global.username>. 
* Update the the folder properties Name: gitUserEmail Value: <git --config global.email>. 
* Update the the folder properties Name: sonarHostURL Value: <GIT Repo URL if using GIT>. 
* Update the the folder properties Name: sonarProjectKey Value: <Name of SonarProject (if using Sonar)>
* <b>Click the folder Credentials</b>
* Update the authToken to the Boomi API Token (Format) <b>BOOMI_TOKEN.user@company.com:bOomi-aPi-ToKen-</b>
* Update the sonarToken
* Update the gitRepoURL<If the gitRepo has username and password>
* Click Rename and rename the folder name to Account_YOUR ACCOUNT

## Run your first Job
Click on the Account folder, select the the Publish Reports tab 
Click on List Atoms Job
And click on Build Now
Once the build is compelete open refresh the output and select the html report

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
|Update Process Schedule Status |Update Process Schedule Status of a single process |
|Update Shared Server |Update shared webserver details of a given Atom |

# Configuring Another Boomi Account on the same Jenkins
You can clone the existing Boomi Folder and change the required Account properties to configure a new Account for Boomi CI/CD on the same Jenkins folder.

# Support
This image is not supported at this time. Please leave your comments at https://community.boomi.com/s/group/0F91W0000008r5WSAQ/devops-boomi
