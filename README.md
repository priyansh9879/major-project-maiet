# Project Description:

The dictionary defines automation as “the technique of making an apparatus, a process, or a system operate automatically.” We define automation as "the creation and application of technology to monitor and control the production and delivery of products and services. Automation can be found in nearly every industry, ranging from transportation and utilities to defines and facility operations. The most prevalent area, however, is undoubtedly manufacturing. With many required tasks being labour intensive or highly repetitive, the creation of automated machinery has improved efficiency and also created greater quality control.

In this project, the main focus is to upscale the Automatic Deployment of website in a webserver with high scalability and high availability anytime and anywhere.

## Prerequisites:

Before Starting, Let’s Talk about the Softwares, Files and Tools we gona need to successfully build this Interesting use case:

## Softwares:
* VirtualBox (Version 6.0)
* Red Hat Enterprise Linux Version 8 (RHEL8)

## Programming Language:
* Python
* Web Technology (HTML, CSS, Node JS)
* Bash Shell Scripting.
* Groovy Script.

## Webserver:
1.	Apache with PHP and JS Installed

## DevOps Tools:
* Git and GitHub
* Docker
* Jenkins

Now, lets Start. Initially, we are aiming to upscale the Automatic Deployment of webserver. If we talk about any initial system, it is sometime tricky and time consuming to install all the requirements inside the OS. For Example, if we would like to Install all the DevOps Tools Like Git, Jenkins, Docker etc., then we need some extra time to toggle over the google and find the correct version for the correct OS. So, in that case, the need of automation is must.

For installing all the requirements in the RHEL8 system, we First have to install the Rhel8 Virtual Machine. For Installation of VirtualBox, we need 3 Things.

1.	VirtualBox6.0 Setup
2.	VirtualBox6.0 Extension Pack
3.	Rhel8 ISO DVD

For Proper Installation of RHEL8, you can Refer the PDF’s Given in the rhel8-data folder inside my Git Repository link Given Below:

[major-project-maiet](https://github.com/priyansh9879/major-project-maiet.git)

Inside this pdf, you will get to know everything about the complete installation of RHEL8 VM. Moving further, after installation of RHEL8 Completely, the Second Requirement is to Install the Git, Docker and Jenkins in the VM. Before installation, lets understand why we are using Git, Docker and Jenkins in our Project

## Git and GitHub:

Git is a VCS — Version Control System. What that really means is, Git helps us manage our project files. One of the primary things that git does and also the primary reason it exists is to keep track of the entire history of things that you are working on.

This is especially helpful for software developers because when you are working on a project you first build a basic version of it and then try to improve it by adding new features (or) just experiment with things. This whole process of experimenting with new features is incredibly error prone and you might want to revert back to your original code.
This is where Version Control comes into play, it automatically tracks every minute change in your project and allows us to revert back to a previous version no matter how many times you changed your files.

Another awesome thing that Git allows to do is, it allows people to work together on the same project at the same time without disturbing each other’s files. Collaboration is all the easier with Git. Team members can work on different features and easily merge changes.

Git is easy to learn and has a lightning fast performance. It outclasses other Version Control Systems like Subversion with features like cheap and local branching, convenient staging areas and multiple workflows.

---

Docker:
Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. Containers allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and deploy it as one package. By doing so, thanks to the container, the developer can rest assured that the application will run on any other Linux machine regardless of any customized settings that machine might have that could differ from the machine used for writing and testing the code.

In a way, Docker is a bit like a virtual machine. But unlike a virtual machine, rather than creating a whole virtual operating system, Docker allows applications to use the same Linux kernel as the system that they're running on and only requires applications be shipped with things not already running on the host computer. This gives a significant performance boost and reduces the size of the application.

In our Project, we will use Docker as a Microservice (DaaMS) for Orchestrating the Webserver inside it. It will reduce the memory, space and time.

---

Jenkins:
Jenkins is an open-source automation tool written in Java with plugins built for Continuous Integration purposes. Jenkins is used to build and test your software projects continuously making it easier for developers to integrate changes to the project, and making it easier for users to obtain a fresh build. It also allows you to continuously deliver your software by integrating with a large number of testing and deployment technologies.

With Jenkins, organizations can accelerate the software development process through automation. Jenkins integrates development life-cycle processes of all kinds, including build, document, test, package, stage, deploy, static analysis, and much more.

Jenkins achieves Continuous Integration with the help of plugins. Plugins allow the integration of Various DevOps stages. If you want to integrate a particular tool, you need to install the plugins for that tool. For example, Git, Maven 2 project, Amazon EC2, HTML publisher etc.

---

Now, we have a Better Understanding of all the Tools. So, without wasting any time, if we want to install all the requirements Successfully, I had provided some Bash Scripts named deploy_jenkins.sh, deploy_docker.sh and deploy_git.sh in the following GitHub Repository.

[major-project-maiet](https://github.com/priyansh9879/major-project-maiet.git)

The Automation Scripts is a Simple Bash Shell script to perform the Complete Installation Process without hassling about the Compatibility and Knowledge of Linux Kernal.

In order to run the scripts, Simply Clone the GitHub Repo, and Run the Following Command:

''' [root@localhost major-project] # ./deploy_docker.sh
[root@localhost major-project] # ./deploy_jenkins.sh
[root@localhost major-project] # ./deploy_git.sh
'''

## Development in Action:

In Our Project, we gona use Jenkins to automate all of our Builds and sync them together to achieve a High Availability and High Scalability. So, Lets Understand the Problem Statement and the Use-case we have to create:

1. From Developer Team, we have Got a Website Code including HTML, CSS, NodeJS Scripting for our website. Developer has also provided us with the GitHub Repository Link where he has stored all the requirement files including the file for creating a CI/CD Pipeline using a Script written in Groovy language.

2. From Developer Team, we have to create a Deployment or Complete CI/CD Pipeline in which we have to create the following jobs in a Sequence

3. Job1 - Whenever the Developer Commit the Code after every Bug Fix, Jenkins will be able to Track the Repository every minute for the changes. As soon as Jenkins found some changes in the repository, it will automatically download the Code to some folder in the server.

4. Job2 - After getting the Code, Jenkins will be able to start the Interpreter as a Container by looking at the Quality and type of the code. (Eg – if code is of HTML, php etc., then it will launch a webserver). After Successful Completion of this Task, Jenkins will be able to Send and Email to the Operational Team about the Successful Creation of the Container.

5. Job3 – After Successful Launch of webserver, the next Task for Jenkins is to Report about the Functioning of the website to the Production Team whether is it working or not. The complete report must be sent in the form of output Generated by the Jenkins Console. If Jenkins will find any error in the Deployment, it will send an Email to the Developer to Re-check the complete Code and Commit the Code again after fixing all the Bugs.

6. Job4 – Last and Final Job is to Monitor the Container the Continuously. In any case, if the Container goes down, it will get automatically started. If the Container get deleted or Corrupted, it will launch a new Container with all the same Content same as in the previous Container.

## Groovy Script for the Jobs we gona create in Jenkins:

'''
job("Job1-git_pull") {
description ("Pulls the code from GitHub")
  scm{
    github('priyansh9879/major-project-maiet','master')
  }
  triggers {
        scm('* * * * *')
    }
  steps {
    shell('sudo cp -rvf * /root/project_files/')
  }
}

job("Job2-deploy_webserver") {
description ("Deploy the code In the webserver")
  triggers {
    upstream('Job1-git_pull','SUCCESS')
    }
    steps {
      shell('''
if sudo ls /github | grep .html
then
    sudo docker pull priyansh9879/centos-apachephp:8
    if sudo docker ps -a | grep webserver
    then
        if sudo docker ps | grep webserver
        then
            echo Container is Already Running
        fi
        echo Starting Exisiting Container http-webserver
        sudo docker start webserver
        sleep 2s
    else
        echo Building Container webserver
        sudo docker run -dit --name webserver -v /root/project_files/:/var/www/html/ -p 81:80 priyansh9879/centos-apachephp:8
    fi''')
    }
    publishers {
    extendedEmail {
      recipientList('mittalsudhanshu29@gmail.com')
      defaultSubject('Container Created Successfully')
      defaultContent('Team Production, This Email is Generated to Inform you that your Webserver is Successfully Deployed. You can check your website using your VM IP_address at Port 81')
      contentType('text/html')
      triggers {
        success
      attachBuildLog(true)
        subject('Deployment Successfully')
        content('Container is Successfully Deployed')
        sendTo {
          developers()
          }
        }
      }
    }
  }
}

job("Job3-Testing_and_sending_report") {
description ("Test and code and send the report to developer")
  triggers {
    upstream('Job2-deploy_webserver','SUCCESS')
    }
    steps {
      shell('''
IP="http://$(sudo docker inspect -f '{{ .NetworkSettings.Networks.bridge.IPAddress}}' webserver):80"
echo $IP
if sudo curl -s -o /dev/null -w '%{http_code}\n' $IP | grep 200
then
        echo "website is Responding Properly"
        exit 0
else
        echo "Website is not Responding Properly"
        exit 1
fi''')
    }
  publishers {
    extendedEmail {
      recipientList('mittalsudhanshu29@gmail.com')
      defaultSubject('Build Failed')
      defaultContent('Dear Team Developer, this email is generated to inform you that the build has Failed. Please Find the Attested Logs Below')
      contentType('text/html')
      triggers {
        failure{
      attachBuildLog(true)
        subject('Failed Build')
        content('The build was failed')
        sendTo {
          developers()
          }
        }
      }
    }
  }
}
'''

For Building a Sed Job, go to (New Item>Give Name – Sed Job>Choose Freestyle project) and configure. Now, after Creating the Complete Sed Job, all we need is to just build the Job. Click on Build and see the creation in action. After waiting for some time, we will get the Email in our Mail that Server is successfully Deployed and is running. We can also check the website like:
 

So Finally, we have ended up with the project.
