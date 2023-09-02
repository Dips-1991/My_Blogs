---
title: "🧛‍♂️ Jenkins Declarative Pipeline with - Docker,🐳 GitHub,🔀 Webhook🔗"
datePublished: Thu Aug 24 2023 11:41:55 GMT+0000 (Coordinated Universal Time)
cuid: cllp3g0pn000n08mlgxtmeswz
slug: jenkins-declarative-pipeline-with-docker-github-webhook
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692871305902/124ecc2e-0152-4922-b63c-bbcc86bbbc8e.jpeg
tags: github, cicd, jenkins-devops, github-webhook, jenkins-pipeline

---

Day 27 Task Of 90DaysOfDevOps Challenge

### ***🎆Introduction***

As of now, we are familiar with the `Jenkins Declarative Pipeline` Also, we are pretty familiar with `Docker` and `Git`, `GitHub` .

In this blog, we are deep dive into the Integration of `Docker`, `GitHub` , `Webhook` with Jenkins and we will take our skills to the next level.

### 🧛‍♂️🐳***Create Jenkins Declarative Pipeline with - Docker and GitHub, Webhook***🔗🔀

In this section, we are going to create a Jenkins Declarative Pipeline with Docker to host our application in a Docker container and GitHub to get the application code from the GitHub repository.

### 🔑**Prerequisite**

Make sure the following tools are installed and running in your system. Here we require the following tools...

🧛‍♂️`Jenkins:` To create the Jenkins Declarative Pipeline. Check out the link to install Jenkins. [https://deepakcloud22.hashnode.dev/day-22-getting-started-with-jenkins](https://deepakcloud22.hashnode.dev/day-22-getting-started-with-jenkins)

🐳`Docker:` Run the docker container to host our application. Check out the link to install docker [https://deepakcloud22.hashnode.dev/day-16-task-docker-for-devops-engineers-part-1](https://deepakcloud22.hashnode.dev/day-16-task-docker-for-devops-engineers-part-1)

🏢`Docker Hub` : To push the Docker image into the Docker Hub repository. Check out to create the Docker-Hub account [https://docs.docker.com/docker-id/](https://docs.docker.com/docker-id/)

🏢`Git/GitHub Repo:` To get the application code from the GitHub [https://www.linkedin.com/pulse/day-8-task-basic-git-github-devops-engineers-deepak-patil/](https://www.linkedin.com/pulse/day-8-task-basic-git-github-devops-engineers-deepak-patil/)

📝`Application Code:` We will use the below application code you can clone the code or fork this repository [https://github.com/Dips-1991/django-notes-app.git](https://github.com/Dips-1991/django-notes-app.git)

### ⏭️***Create The Pipeline***

1. First, we will create the Pipeline. As we have installed Jenkins in our system.
    
2. Navigate to the Jenkins home page and `click` on `New Item` .
    
3. Enter `name` of the job.
    
4. Select the `Pipeline` as a project and click on `Ok` .
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692733762021/c2fe4746-a19d-4d2c-ad34-323c645c62d8.png align="left")
    
5. Enter the `Description.`
    
6. Select the `GitHub project` As we know we are integrating GitHub with Jenkins and adding the GitHub repo URL to the `Project url` As we know our application code is present on GitHub.
    

### 🔧***Configure The Pipeline***

Now, come to our main task here we will write the Ddeclerative pipeline Groovy syntax code.

### 🧬***Clone Stage***

1. `Pipeline section:` In the `Definition` select the `Pipeline script` from the drop-down.
    

### 🛠️***Build Stage***

1. `Script section:` Under `stages` in the first `clone` `stage` we are cloning the code. To clone the code we have to use the `GitHub URL` and the `Branch Name` where our code is present.
    
2. `git url:"<github-repo-url>,<branch-name>"`
    
3. In the second `Build` `stage` we are building the docker image using the Dockerfile. Here we have to use `Groovy syntax` to run the docker command with the help of `sh.`
    
4. `sh "docker build -t Django-app-image ."`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692724583446/8e7b260e-d149-4524-81af-718c3cc6bc4c.png align="left")
    

### 🚀***Push Stage &Configuring The DockerHub Credentials***

1. In the this `stage`, we are pushing the image to DockerHub. For that First, we will save our credentials in Jenkins and we are associate them with the `ID`.
    
2. As we are aware that exposing the credentials is how dangerous so, we are using here the Jenkins environment variable.
    
3. Navigate to the `Manage jenkins --> Security --> Credentials`
    
4. Click on the `System` under the `Stores scoped to Jenkins`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692725527240/6c6c52c9-f307-4185-8f9f-085403e12761.png align="left")
    
5. Once, you click on the System you will navigate to the next page where you have to click on `Global credentials (unrestricted)` .
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692725713449/597644d7-dffc-4edc-92c0-a93b73a29ee3.png align="left")
    
6. Once you click you will navigate to the next page click on `Add credentials.`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692725847202/11c4118d-b623-42fb-82ca-f24e6adeb62b.png align="left")
    
7. Once, you click on `Add credentials` .You will navigate to the next page where we will store our `DockerHub credentials.`
    
8. Here in `Kind` select `Username with password` from the dropdown. As we are using DockerHub credentials.
    
9. Keep `Scope` as it is.
    
10. In the `Username` add the `DockerHub Username` .
    
11. In the Password add the `DockerHub Password` .
    
12. Keep `Treat username as secret` uncheck.
    
13. Enter the `ID (credentials are associate with ID)` name at your convenience. Then `ID` We will use in our code to fetch the username and password. `Click on Create` .
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692726630989/c2b9a1f9-69b9-462b-852b-542f3d51345b.png align="left")
    
14. Now you will see the credentials are added.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692726778239/a4cfa7db-c2ec-4a01-8c4a-e180ae19231f.png align="left")
    
15. In the `Push Image` `stage` We will push the image to DockerHub with the help of `withCredentials` function and will pass the `credentiasId`, `usernameVariable`, `passwordVariable` to the `"usernamePassword"` function.
    
    1. `withCredentials([usernamePassword(credentiasId:"<your-credentials ID>",usernameVariable:"<any-name>",passwordVariable:"<any-name>")])`
        
    2. In the next command, we have to tag our created image with the DockerHub username.
        
        `sh "docker tag <image-name> $env.<usernameVariable>/<new-image-name:<tag>>"`
        
    3. In the next command, we will `login` to the DockerHub
        
        `sh "docker login -u ${env.dockerUsername} -p ${env.dockerPassword}".`
        
    4. In the next command, we will push the image into the DockerHub.
        
        `sh "docker push $env.<usernameVariable>/<new-image-name:<tag>>"`
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692738121131/7f3e348b-0834-4a83-afff-daf3abccc632.png align="center")
        

### 🏭***Deploy Stage***

1. In this `stage`, we are deploying our application into the Docker container using `docker-compose` the file.
    
    `sh "docker-cmpose down && docker-compose up -d"`
    
2. Make sure `docker-compose` is installed in your system.
    
3. Here we have to replace your `image name` in `image` statement in `Docker-Compose File`, Image that you have pushed into the `DockerHub`. Our `Compose-File` will fetch that image from `DockerHub.`
    
4. Also, we are exposing the `ports` here `(host-port:container-port)` in the `ports` statement.
    
5. Here is the `Docker-compose` file.
    
    ```apache
    version : "3.3"
    services :
      Web :
         #Image which we have pushed into DockerHub
         image : deepak1603/django-app-image:v1
         ports :
             - "8000:8000"
    ```
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692806612193/7be818a5-aeba-4ffa-a6bd-568d7b7864c2.png align="left")
    
6. Now, In the final step click `Apply and Save` .
    

### ⚙️***Execute The Pipeline***

1. Now, Go to the Dashboard/Create project pipeline and click on Build Now.
    
2. The `pipeline execution` will start ...Code will be `Colning` from `GitHub`, `Docker image` will be created, `Image tagging` will be happening, `DockerHub login` will be happening, and `Pushing image into DockerHub` will be happening and finally, the `Docker Container` will be created with a single click .......Let's see the magic.
    

### ⚠️***Error - 1***

1. Once built here we are not able to build successfully because we have given the image name in capital letters see the below error.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692735238664/d975c386-296e-4f09-b669-752a49205935.png align="left")
    
2. So we are changing the `Image Name` here with `django-app-image` Wherever applicable click on `Apply and Save.`
    
    ```apache
    sh "docker build -t django-app-image ."
    ```
    
3. Now after saving click on `Build Now.` again.
    

### ⚠️***Error - 2***

1. Now, here we got another error which is regarding the `Permission denied` because `Jenkins User` is not part of the `Docker Group.`
    
2. We have to add `Jenkins User` into the `Docker Group` and Reboot the system
    
3. Run the below command in the terminal.
    
    ```apache
    sudo usermod -a -G docker jenkins 
    sudo systemctl reboot
    ```
    
4. Now after adding `Jenkins User` to the `Docker Group` .
    
5. Now after saving click on `Build Now.` again.
    

### ⚠️***Error - 3***

1. Now, here we are getting one more error `withCredentials step must be called with a body`.
    
2. So make sure `withCredentials` is a function as we know, so we have to write the code inside the `{ }` brackets.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692805391902/3d339543-1ef1-45e6-98c3-fc72bec164fe.png align="left")
    
3. Here is the updated code of the `withCredentials()` function.
    
    ```apache
    withCredentials([usernamePassword(credentialsId:"DockerHubCredentials", passwordVariable:"dockerPassword", usernameVariable:"dockerUsername")])
       {
       sh "docker tag django-app-image ${env.dockerUsername}/django-app-image:v1"
       sh "docker login -u ${env.dockerUsername} -p ${env.dockerPassword}"
       sh "docker push ${env.dockerUsername}/django-app-image:v1"
       }
    ```
    
4. After updating the changes again click on `Build Now`. And let's see this time.
    

### 👏🎉🏆***Successful Execution*** 🌟💯

Now, Finally, we are running our pipeline successfully you can see the `Console output` also the `Pipeline Stage View` .

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692808064390/b2b98666-b110-4ef3-8b96-36c865305e9e.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692810532840/190197a0-2507-4814-8e98-9f6c1c4eba54.png align="left")

We are able to push the `image` into `DockerHub.`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692808129307/482ba9aa-0aa9-43bf-a611-424092d5339f.png align="left")

Now finally we can check whether the Docker container is created or not.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692808212663/652ade57-d3d9-4d00-99cf-8662224e0ac5.png align="left")

🕺🕺👏👏🎉🎉 BoooooooooooooMMMM we are able to deploy the application successfully.

Now it's time to access our application from the browser.

To access the application copy the EC2 instance IP Address and paste it into the browser along with `:8000`, Because our application is running on `Port 8000` .

🕺🕺👏👏🎉🎉 BBBBBBBoooooooooooooMMMMMMMMMMMMMM we have successfully deployed our application using the Jenkins pipeline.🕺🕺👏👏🎉🎉

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692809853548/0868accf-8b9b-4101-82bf-0b875e75d2e1.png align="left")

### 🔝***CI/CD Automation***

Now, it's time to make our Jenkins pipeline fully automated.

As of now, we are writing our pipeline code into the `Jenkins script section`.

Now, we will save our `script code` into `GitHub` also in the form of `Jenkinsfile.` and we are fetching the script code from GitHub instead of writing it into Jenkins.

Here is the `Jenkins file(same above script code)`. We will store it at `GitHub` in the application code itself.

Here is the Jenkins file we will store on GitHub in the application code itself.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692810974108/4443b2d6-d8ac-4dd4-b850-799709999f9f.png align="left")

### 📦***Executing the Jenkins File from GitHub***

To Call `Jenkins file` From Jenkins, we have to make some modifications in the configure section shown below.

1. Goto `Dashboard` and click on `Application Pipeline.`
    
2. Goto `Pipeline` in `Definition` select `Pipeline script from SCM` .
    
3. Under `SCM` select `Git`.
    
4. Under `Repositories` enter the `GitHub URL.`
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692811124775/3071fe2a-f10f-41c5-9e41-9931201be4c2.png align="left")
    
5. In `Brach Specifier` under `Branches to build` Enter your branch name in my case it is `main.`
    
    In `Script Path` enter the `Jenkinsfile` as path then click on `Apply and`
    
    `Save` .
    

### 🏗️***Automate Deployment Using GitHub-Webhook***

Now, comes to the `CI/CD Automation Using GitHub Webhook` .

We will configure our `Jenkins file` to be executed after any changes are updated in the `GitHub Repository.`

To make it possible we will use here the Github Webhook.

1. Go to the Pipeline configure page in `Build Triggers.`
    
2. Select the checkbox `GitHub hook trigger for GITScm polling` Click on Apply and Save.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692812509782/3a685907-261a-4b06-9aa2-a31c09de7a02.png align="left")
    
3. Also, we required `GitHub Integration` plugin got to plugin and install the required plugin.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692812935676/3cd8f7e4-c1d5-47b9-9cdf-f0ec6eafdf6f.png align="left")
    

### 🔗***GitHub-Webhook Configuration***

1. Go to your `GitHub repository` and click on `Settings.`
    
2. Click on `Webhooks` and then click on `Add webhook.`
    
3. In the `Payload URL` field copy and paste your `Jenkins environment URL`. and at the end of this URL add `/github-webhook/`
    
4. In the `Content type`select: `application/json` and leave the `Secret` field `empty`.
    
5. In the `Which events would you like to trigger this webhook?` section select as per your requirement and click on `Add webhook.`
    
6. `Refresh` the page until you will get the `Right sign` ✔
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692813115247/4f121640-f348-44d2-accf-6276f473a082.png align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692813611688/52363534-1c60-4e97-bf9f-395c8b2025ab.png align="left")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692813914530/5daf42c6-8607-4cd0-827c-14e80bed0e36.png align="left")
    

### ✔🔗***Checking The WebHook Integration***

We will Change the title from `TVS Jupiter Is Amazing` to `DevOps is Amazing` .

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692818987785/562c8431-621d-4602-a480-f8d36a81da3c.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692819101874/17122caf-a6ba-4658-9bec-14a2d84c31be.png align="left")

After we had changed the code in the repository and committed the changes the `magic happens` 🕺🕺👏👏🎉🎉... Our Job build execution starts without clinking on `Build Now.`

`WebHook` is `added to trigger` `execution of Jenkins jobs` *based on* `GitHub events`*.* If anyone in the developer team changes the code, it will automate the `Build Now process` .

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692819748026/9cb58803-0111-4a2b-8a05-0e5ced213cf4.png align="left")

### **✨Conclusion**

✔In this post, we combined GitHub Jenkins Declarative Pipelines and Docker for enhanced CI/CD.

✔We used the `sh` command to run Docker commands within pipeline stages.

✔Then, we explored Docker Groovy syntax in the `script` block for smoother image creation and container handling.

✔We have done troubleshooting.

✔We have learned about Jenkinsfile

✔We have implemented the Wbhook call successfully.

*Check Out the Video for Complete CI/CD Using Jenkins, Docker, GitHub, and Github-Webhook.*

%[https://www.youtube.com/live/AaVO1Mvr3q4?si=T-AhqSXvIAVtbCba] 

---

> **Thank you🙏🙏... for taking the time to read this blog. I hope you found the information helpful and insightful. So please keep yourself updated with my latest insights and articles on DevOps 🚀 by following me on**
> 
> So, Stay in the loop and stay ahead in the world of DevOps!
> 
> ***Happy Learning !... Keep Learning ! 😊***