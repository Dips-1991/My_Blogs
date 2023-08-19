---
title: "Day 26:  Jenkins Pipelines: A Guide to Declarative Pipelines and Groovy Syntax 🔄"
datePublished: Sat Aug 19 2023 20:21:46 GMT+0000 (Coordinated Universal Time)
cuid: clligtaj3000209mb0k5y0ec8
slug: day-26-jenkins-pipelines-a-guide-to-declarative-pipelines-and-groovy-syntax
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692476254447/2509ebb6-c4b5-4bde-9399-9c71d01a572c.webp
tags: jenkins-devops, jenkins-installation, jenkins-pipeline, jenkins-declarative-pipeline, declarative-vs-scripted

---

### 🎆 ***Introduction***

One of the most important parts of your DevOps and CICD journey is a Declarative Pipeline Syntax of Jenkins using which we can create our pipeline as a code that brings automation to your development, building, testing, monitoring deploying/delivering of the application process.

### 💡 ***Understanding Pipelines***

The pipeline is the process in Jenkins where we can provide the steps/job that are interlined and executed in the specific order to perform the entire CI/CD task and make the entire process automated

### 📝***Scripted Pipelines vs.*** 📜***Declarative***

👉 There are two types of pipelines used in Jenkins to create the Jenkins pipeline as a code

### 📝 ***Scripted Pipeline***

* Scripted Pipeline is the original pipeline syntax for Jenkins, and it is based on the `Groovy scripting language`.
    
* In Scripted Pipeline, the entire workflow is defined in a single file called a Jenkinsfile.
    
* A scripted Pipeline provides a lot of flexibility and control over the workflow, but it can be more complex and verbose than Declarative Pipeline.
    
    Here is an example of a simple Scripted Pipeline:
    
    ```apache
    node {
        stage('Build') {
            // Build the application
            sh 'mvn clean install'
        }
        stage('Test') {
            // Run the tests
            sh 'mvn test'
        }
        stage('Deploy') {
            // Deploy the application
            sh 'deploy.sh'
        }
    }
    ```
    

### 📜 ***Declarative Pipeline***

* Declarative Pipeline is a more recent addition to Jenkins and provides a more structured and simpler syntax for defining pipelines.
    
* Declarative Pipeline is based on the Groovy programming language, but it uses a Groovy-based DSL (Domain-Specific Language) for pipeline configuration.
    
* The main benefit of a Declarative Pipeline is its readability and ease of use.
    
    Here is an example of a simple Scripted Pipeline:
    
    ```apache
    pipeline {
        agent any
        stages {
            stage('Build') {
                steps {
                    // Build the application
                    sh 'mvn clean install'
                }
            }
            stage('Test') {
                steps {
                    // Run the tests
                    sh 'mvn test'
                }
            }
            stage('Deploy') {
                steps {
                    // Deploy the application
                    sh 'deploy.sh'
                }
            }
        }
    }
    ```
    

### 🤔***Why you should have a Pipeline***

A Pipeline is a user-defined model of a CD pipeline. A Pipeline’s code defines your entire build process, which typically includes stages for building an application, testing it, and then delivering it.

The definition of a Jenkins Pipeline is written into a text file (called a [`Jenkinsfile`](https://www.jenkins.io/doc/book/pipeline/jenkinsfile)) which in turn can be committed to a project’s source control repository.

### 🔄 ***Pipeline syntax And It's Explanation***

👉 Here, is the sample code of the `Declarative Pipeline` in Jenkins

```apache
🔄pipeline {
    agent any
    environment {
        // 🌍 Define environment variables here
    }
    parameters {
        // 🎛️ Define pipeline parameters here
    }
    stages {
        stage('Build') {
            steps {
                // 🏗️ Build your application here
            }
        }
        stage('Test') {
            steps {
                // ✅ Run tests
            }
        }
        stage('Deploy') {
            steps {
                // 🚀 Deploy your application
            }
        }
    }
    post {
        success {
            // 🎉 Actions for successful run
        }
        failure {
            // 😞 Actions for failure
        }
        always {
            // 🔄 Actions to run regardless of success or failure
        }
    }
}
```

👉 ***Here's an explanation of each section:***

* `pipeline`: This is the top-level block that defines the entire pipeline.
    
    * `agent`: Specifies where the pipeline will run. In this case, `any` this means it can run on any available agent or on Jenkins slave.
        
    * `environment`: Defines environment variables that can be used throughout the pipeline.
        
    * `parameters`: Defines parameters that can be passed to the pipeline when triggering it manually.
        
    * `stages`: This block is where you define the different stages of your pipeline.
        
        * `stage`: Defines individual stages within the pipeline. here individual stages are `Build, Test, Deploy`
            
            * `steps`: Within each stage, you define the specific steps or actions to be executed.
                
* `post`: This block contains actions to be taken after the stages have run.
    
    * `success`: Defines actions to be taken if the pipeline run is successful.
        
    * `failure`: Defines actions to be taken if the pipeline run fails.
        
    * `always`: Defines actions to be taken regardless of whether the pipeline run succeeds or fails.
        

### **📖 *Task: Create a New Job using Declarative Pipeline- Hello World Example***

Here, in this example, we will create and execute the simple pipeline as code step by step

As we know how to install Jenkins in the Ubuntu OS. To know more about installing Jenkins please check my blog

[https://deepakcloud22.hashnode.dev/day-22-getting-started-with-jenkins](https://deepakcloud22.hashnode.dev/day-22-getting-started-with-jenkins)

👉 ***Let's do our task........👇***

1. Navigate to the Jenkins home page and `click` on `New Item` .
    
2. Enter the name of the job.
    
3. Select the `Pipeline` as a pipeline and click on `Ok` .
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692473079222/85ba87a0-7a46-43e8-93bd-b8efcad04cf5.png align="center")
    
4. Provide the description if required.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692473211460/7b7ff271-23dc-4cc2-968b-ff1020cb5d34.png align="center")
    
5. Navigate to the `Pipeline` section.
    
6. In the `Definition` select the `Pipeline script` .
    
7. In the `Script` write your pipeline `groovy` syntax code as below.
    
    ```apache
    pipeline{
        agent any
        stages{
            stage("Build"){
                steps{
                    echo "Hello DevOps World...."
                }
            }
           
        }
    }
    ```
    
8. Click on `Apply` and `Save` .
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692473930882/47c70178-597e-4fea-86f0-aed5fef6b2fd.png align="center")
    
9. You can see the pipeline is created at the Jenkins Dashboard.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692474065423/18707af6-0b70-4c1b-b5a0-b02b978cca1d.png align="center")
    
10. Now click on the newly created job and on the left side click on `Build Now` to execute the pipeline.
    
11. Once you click on the `Build Now` you can see the execution of the job in `Stage View`
    
12. To see the output of the job click at the bottom of the left-side `BUILD_NUMBER` which is `#1` in my case
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692474855451/60a8652c-3d48-48bb-96ab-d5339056efc1.png align="center")
    
13. Once you click on `BUILD_NUMBER` then you will redirect to the `Build Number` page.
    
14. Click on `Console Output` it to see the output of the Job.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692475250353/c7ef4264-57c6-4d07-b3c5-db23668edde1.png align="center")
    

Congratulation <sup>😎😎</sup> 💐💐 you have successfully created and executed your first Declarative Jenkins Pipeline 🎉🎉.

### ***🎆*** ***Conclusion***

In this example, we have learned How Jenkins Declarative Pipelines lay the foundation for seamless CI/CD workflows.

By dissecting each stage, step, and action, we've defined in the process of pipeline creation. 🌈 Embrace the power of Groovy, and let the structured syntax guide you toward creating pipelines that elevate your development endeavors. Remember, with every step you take, you're inching closer to mastering the art of efficient software delivery! 🚀🎉

---

> **Thank you🙏🙏... for taking the time to read this blog. I hope you found the information helpful and insightful. So please keep yourself updated with my latest insights and articles on DevOps 🚀 by following me on**
> 
> So, Stay in the loop and stay ahead in the world of DevOps!
> 
> ***Happy Learning !... Keep Learning ! 😊***