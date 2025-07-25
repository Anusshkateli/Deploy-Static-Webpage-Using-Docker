Deploy Static Webpage Using Docker
This guide will walk you through the process of packaging a static website into a Docker image, defining the web server environment using a Dockerfile, and deploying the website to a Docker container. Finally, you'll learn how to push your custom image to Docker Hub.

Prerequisites
Before you begin, ensure you have the following installed:

Docker Desktop: This includes Docker Engine, Docker CLI, and Docker Compose.

Download Docker Desktop

Step 1: Prepare Your Sample Website
Create a simple static website. For this guide, let's assume your website files (e.g., index.html, style.css, script.js) are located in a folder named SampleWebSite.

Example SampleWebSite/index.html:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Static Website</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
            background-color: #f0f0f0;
            color: #333;
        }
        h1 {
            color: #007bff;
        }
        p {
            font-size: 1.2em;
        }
    </style>
</head>
<body>
    <h1>Welcome to My Dockerized Website!</h1>
    <p>This is a simple static page served by Nginx in a Docker container.</p>
    <img src="https://placehold.co/468x120/E89D82/558558?text=Your+Website+Image" alt="Sample Image" style="border-radius: 8px;">
</body>
</html>

Step 2: Verify Docker Installation
Open your terminal or command prompt and run the following commands to check your Docker installation and version.

docker --version
```bash
docker info

To get the Docker info in JSON format:

docker info --format '{{json .}}'

Step 3: Pull the Nginx Latest Image
Nginx is a popular web server that we'll use to serve our static website. Pull the official Nginx image from Docker Hub.

docker pull nginx:latest

Verify that the image has been downloaded:

docker images

You should see nginx listed in your images.

Step 4: Create a Dockerfile
A Dockerfile is a script that contains a series of instructions for building a Docker image. Create a file named Dockerfile (no extension) in the root directory of your project, next to your SampleWebSite folder.

# Use the official Nginx image as the base image
FROM nginx:latest

# Copy your static website files into the Nginx default web directory
# The `.` refers to the current directory where the Dockerfile is located (your project root)
# So, it copies the `SampleWebSite` folder and its contents.
# Nginx serves content from /usr/share/nginx/html/ by default.
COPY ./SampleWebSite/ /usr/share/nginx/html/

# Expose port 80, which Nginx listens on by default
EXPOSE 80

Step 5: Build the Docker Image
Navigate to your project's root directory in the terminal (where your Dockerfile and SampleWebSite folder are located). Then, build your Docker image.

docker build -t my-static-website:1.0 .

-t my-static-website:1.0: Tags your image with the name my-static-website and version 1.0. You can choose any name and tag.

.: Specifies the build context (the current directory), meaning Docker will look for the Dockerfile and copy files from here.

After the build completes, verify your new image:

docker images

You should now see my-static-website listed.

Step 6: Run the Docker Container
Now, run a container from your newly built image. This will start the Nginx web server and serve your website.

docker run -d -p 8080:80 --name my-website-container my-static-website:1.0

-d: Runs the container in detached mode (in the background).

-p 8080:80: Maps port 8080 on your host machine to port 80 inside the container (where Nginx is listening). You can choose any available host port.

--name my-website-container: Assigns a readable name to your container.

my-static-website:1.0: The name and tag of the image you want to run.

Verify that your container is running:

docker ps

Step 7: Access Your Website
Open your web browser and navigate to:

http://localhost:8080

You should see your static website displayed!

Step 8: Push Image to Docker Hub (Optional)
To share your image or use it on other machines, you can push it to Docker Hub.

Log in to Docker Hub:
First, you need to log in to your Docker Hub account from your terminal. Replace YOUR_DOCKERHUB_USERNAME with your actual Docker Hub username.

docker login

You will be prompted to enter your Docker Hub username and password.

Tag your image for Docker Hub:
Docker Hub image names follow the format your_dockerhub_username/image_name:tag. You need to re-tag your existing image with this format.

docker tag my-static-website:1.0 YOUR_DOCKERHUB_USERNAME/my-static-website:1.0

Replace YOUR_DOCKERHUB_USERNAME with your actual Docker Hub username.

Push the image:

docker push YOUR_DOCKERHUB_USERNAME/my-static-website:1.0

This command will upload your image to your Docker Hub repository.

Now, your Docker image is available on Docker Hub for others (or yourself) to pull and use!

This guide provides a comprehensive overview of deploying a static website using Docker, from preparation to deployment and sharing.
