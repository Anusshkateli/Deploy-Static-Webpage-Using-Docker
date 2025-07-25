# Deploy-Static-Webpage-Using-Docker
Download and load nginx
</n>
<img width="468" height="120" alt="image" src="https://github.com/user-attachments/assets/e89d825e-6403-4456-8558-d18e55b15a00" />
Put the sample website in the html folder of nginx
Open local host
Website will be visible on nginx
Install Docker and check vision 
Check info
Convert the Docker info into json format 
Pull latest nginx image 
Check images 
Creating a Docker file with the following contents: FROM nginx: latest 
COPY ./SampleWebSite/ /usr/share/nginx/html/ EXPOSE 80 Building the Docker file 
Check Docker images 
Pushing image to Dockerhub


Docker to package a static website into a Docker image, define the web server environment using a Dockerfile, and deploy the website to a Docker container.

