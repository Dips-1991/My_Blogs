---
title: "🚀 Docker Build Showdown: Regular Docker Build -vs- Multistage Docker Build"
datePublished: Wed Aug 16 2023 13:49:28 GMT+0000 (Coordinated Universal Time)
cuid: clldsh871000009mgby7c5l5e
slug: docker-build-showdown-regular-docker-build-vs-multistage-docker-build
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692035763039/9654c63e-4449-4164-8d51-dcb4dc235178.gif
tags: docker, dockerfile, docker-images, docker-build, multistage-docker-build

---

### 🎆 ***Introduction***

Docker, the superhero of containerization, offers multiple ways to build images. We're pitting the regular Dockerfile build against the multistage Dockerfile build. Who'll emerge victorious? Let's dive into the ring and find out!

### **🤔 *What's the Buzz About Multistage Builds?***

🔍 **Multistage Docker builds** mean using multiple build stages(multiple `FROM` statements) in one Dockerfile to craft a final image. Each stage has its own set of instructions, like a team of superheroes working together!

Multi-stage builds combined with slim base images is the single most effective technique to reduce the size of your Docker images.

### 💡 ***The basic idea behind Docker’s multistage builds***

👉 Usually you’d start out with a fat base image like Ubuntu or an image specific to your programming language. This comes packed with essential build tools like Compilers.

👉 Next, you’d run commands to download necessary dependencies like libraries, testing frameworks, linters, security scanners and so on. All of these are needed for your code to pass necessary quality checks, compile and produce the final artifact(s).

👉 At this point, your application is built and ready to run, so you deploy this image in production.

But we no longer need all those dependencies used during the BUILD phase. If your app is written in C++, you probably only need the compiled binary for production.  
And yet, our prod container carries that 900MB worth of burden with it 👎

So we obviously shed all that load!

But traditionally, this has been very tedious to achieve in Docker, involving hacks, custom bash scripts and lots of spaghetti code to maintain 💢

### 🚶 ***Enter Into The Multi-stage Builds***

These allow you to split your Docker image definition into multiple STAGES. Every time you use a `“FROM <base image>”` statement in your Dockerfile, it's a new stage.

You can cherry-pick the files to include from each stage into your final image. So it’s not a surprise that you’d only pick the final executable file to put into your final image.

You can choose a lightweight base image such as `Alpine or Distroless` and just add your executable to it.

This is the most powerful way to end up with a super light image that is easy to run and maintain in production 🚀

### 👍 ***Advantages of Multistage Docker Builds***

🚀 **Smaller Image Size:** Trim the fat! Multistage builds allow you to discard unnecessary bits, leading to svelte and efficient final images.

🏎️ **Speedy Builds:** Cut to the chase! Multistage builds to speed up the process by having fewer layers and less data to shuffle around.

🛡️ **Enhanced Security:** Shield's up! Unnecessary tools or dependencies used during the build process don't find their way into the final image, minimizing attack vectors.

🚢 **Simplified Deployment:** Lighten the load! With multi-stage builds, you only ship the final image, skipping the hassle of managing intermediary build artifacts.

### 👎 ***Disadvantages of Multistage Docker Builds***

🧩 **Complexity:** It's like building a puzzle. Multistage builds can become complex if not organized well. Debugging might involve understanding each stage's role.

📚 **Learning Curve:** Buckle up for learning! The concept of multistage builds might require extra understanding, especially for newcomers.

### 👉 ***Let's See It in Action!***

Imagine we have a Python Flask app, and we want to utilize multistage builds to optimize our Docker image. Here's a simplified example:

```apache
# Stage 1: Build the base image with Python and Poetry dependencies
FROM python:alpine3.7

# Copy the entire current directory to the /app directory in the image
COPY . /app

# Set the working directory to /app
WORKDIR /app

# Install Python packages from requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# sets an environment variable named PORT with the value 5000.
ENV PORT 5000

# container will expose port 5000
EXPOSE 5000

# Set the entrypoint to "python" as the executable
ENTRYPOINT [ "python" ]

# Run the application app.py 
CMD [ "app.py" ]
```

1. ### ***✔ Build the Dockerfile***
    
    First, we will normally build this Dockerfile, and let's see the final image size after building the image
    
    To build the Docker images use this command:
    

```apache
docker build -t <image-name> .
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692042139845/89766602-cd3b-4ba2-ad4e-f52525293976.png align="center")

👉 Here you can see the final build image size is `98.4MB`

1. ### ***✔ Build the Dockerfile using Multistage-Build***
    
    Here we will now create the multi-stage Dockerfile
    

```apache
# Stage 1: Build Stage
FROM python:alpine3.7 as builder

# Copy the entire current directory to the /app directory in the image
COPY . /app

# Set the working directory to /app
WORKDIR /app

# Install Python packages from requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Stage 2: Production Stage or any 
FROM python:alpine3.7

# Copy the application code and installed packages from the builder stage
COPY --from=builder /app /app

# Set the working directory to /app in the new stage
WORKDIR /app

# Set an environment variable for the application's port
ENV PORT 5000

# Expose the application port
EXPOSE 5000

# Set the entrypoint to "python"
ENTRYPOINT [ "python" ]

# Set the default command to "app.py"
CMD [ "app.py" ]
```

***Explanation:***

1. **Stage 1 (Build Stage):**
    
    * Start with the `python:alpine3.7` base image and name this stage as `builder`.
        
    * Copy the entire contents of the current directory (`.`) into the `/app` directory within the image.
        
    * Set the working directory to `/app`.
        
    * Install Python packages listed in `requirements.txt` using `pip`. We use `--no-cache-dir` to avoid caching pip package metadata.
        
2. **Stage 2 (Production Stage):**
    
    * Start from the same `python:alpine3.7` base image.
        
    * `COPY --from=builder` - Copy the application code and installed packages from the `builder` stage's `/app` directory to the `/app` directory in the current image.
        
    * Set the working directory to `/app` in the new stage.
        
    * Set an environment variable named `PORT` with the value `5000`.
        
    * Expose port 5000 to allow incoming traffic for the application.
        
    * Set the entrypoint to `"python"`. This specifies the default command that will be run when a container starts.
        
    * Set the default command to `"`[`app.py`](http://app.py)`"`, which is the script that will be executed when the container starts.
        

Now, we will build this Multistage Dockerfile, and let's see the final image size after building the image

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1692044848674/c4a0fd27-e2e9-4b4a-83dd-70fc2d44216a.png align="center")

👉 Here you can see the final build image size is `81.3MB`

### 🥯***Distroless images***

Distroless images, often referred to as "distroless" containers, are Docker images that are designed to be as minimalistic as possible. They aim to provide a highly secure and lightweight environment for running applications while significantly reducing the attack surface and potential vulnerabilities that can be exploited by attackers. Distroless images are particularly popular in the context of containerized applications where security and efficiency are critical.

👉 Key characteristics of distroless images include:

1. ***No Operating System:***
    
    ❌🐧 Distroless images intentionally exclude a traditional Linux distribution or operating system components. This means they lack utilities, shells, package managers, and other components commonly found in typical Linux distributions. This minimalistic approach reduces the potential attack vectors that could be exploited.
    
2. ***Only Essential Libraries:***
    
    📚🚫 Distroless images include only the necessary libraries required to run the specific application. Unnecessary system libraries and binaries are excluded, further reducing the image's size and complexity.
    
3. ***Security-Focused:***
    
    🔒🛡️ By reducing the software stack to the bare essentials, distroless images inherently have a smaller attack surface. Fewer components mean fewer potential vulnerabilities that could be exploited by malicious actors.
    
4. ***Smaller Image Size:***
    
    📏💽 Distroless images are known for their small image size compared to traditional images based on full-fledged Linux distributions. This is beneficial for faster image distribution and deployment, especially in environments where bandwidth and storage resources are limited.
    
5. ***Use Case Specific:***
    
    🛠️🧩Distroless images are designed to run specific types of applications, like Java applications, Python applications, or Node.js applications. Each distroless variant is tailored to the requirements of the runtime environment.
    
6. ***Immutable and Stateless:***
    
    🏛️🔄Distroless containers follow the principles of immutable infrastructure and statelessness, aligning with modern container best practices.
    

It's important to note that while distroless images offer enhanced security and efficiency benefits, they might not be suitable for all use cases. Some applications may require specific system utilities or components that are intentionally excluded in distroless images. Additionally, debugging and troubleshooting might be more challenging due to the lack of traditional tools commonly available in full Linux distributions.

### ***🎆 Conclusion***

In the above-explained example -- The multi-stage build helps in creating a smaller production image by excluding unnecessary files and intermediate build artifacts. The `Builder` the stage is used for installing dependencies and the `production` stage contains the minimum required for running the application.

*You can find some Distroless images here...* [https://github.com/GoogleContainerTools/distroless/tree/main](https://github.com/GoogleContainerTools/distroless/tree/main)

*You can find some Distroless images examples here...*

[https://github.com/GoogleContainerTools/distroless/tree/main/examples](https://github.com/GoogleContainerTools/distroless/tree/main/examples)

*Check Out the Video for the Multi-Stage Docker Build...*

%[https://www.youtube.com/watch?v=yyJrZgoNal0] 

---

> **Thank you🙏🙏... for taking the time to read this blog. I hope you found the information helpful and insightful. So please keep yourself updated with my latest insights and articles on DevOps 🚀 by following me on**
> 
> So, Stay in the loop and stay ahead in the world of DevOps!
> 
> ***Happy Learning !... Keep Learning ! 😊***