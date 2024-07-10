# Huddle-landing-page_frontend_project
## Tools & Technology Used:
- Git
- GitHub
- Docker
- Jenkins

## For Creating similar Architecture follow the below steps
### Below are the article/document Links to install the required tools
- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Docker](https://docs.docker.com/engine/install/)
- [Jenkins](https://www.jenkins.io/doc/book/installing/)


### Steps and Setup the project
- **Clone the repo**
```bash
git clone https://github.com/AdityaThorat679/Huddle-landing-page_frontend_project.git
```
Here, we are cloning our repo into our local system to check if the code is running and to add the Dockerfile to it.

- **Dockerfile creation**
```bash
FROM node:22.3.0
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 5000:5000
CMD ["npm", "start"]
```
1. **FROM node:22.3.0**:
    Uses Node.js version 22.3.0 as the base image.
3. **WORKDIR /usr/src/app**:
   Sets the working directory inside the container to `/usr/src/app`.
4. **COPY package*.json ./**:
   Copies `package.json` and `package-lock.json` (if present) from the host to the container.
5. **RUN npm install**:
   Installs Node.js dependencies specified in `package.json`.
6. **COPY . ./**:
   Copies all files from the host to the container.
7. **EXPOSE 5000:5000**:
   Exposes port 5000 on the container to allow connections.
8. **CMD ["npm", "start"]**:
   Specifies the command to start the Node.js application when the container starts.

- **Build Image**
```bash
docker build -t nodejs-app:leatest .
```
This command builds a Docker image named nodejs-app with the tag latest using the Dockerfile found in the current directory.

- **Run Image / Run Container**
 ```bash
docker run -p 5000:5000 nodejs-app:leatest
```
1. docker run: Starts a new Docker container.
2. -p 5000:5000: Maps port 5000 on the host to port 5000 on the container, allowing access to the application running inside the container.
3. nodejs-app: Specifies the Docker image (nodejs-app with tag latest) to use for creating the container.

- **Docker Compose File**
 ```bash
version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"
```
- **version: '3'**: Specifies the version of Docker Compose file format being used (version 3 in this case).
- **services**: Defines the services that make up your application.
  - **web**: Defines a service named `web`.
    - **build: .**: Specifies that the service should be built using the Dockerfile (`Dockerfile`) located in the current directory (`.`).
     - **ports**: Specifies port mappings between the Docker container and the host machine.
       - `"5000:5000"`: Maps port 5000 on the host to port 5000 on the container. This allows you to access the application running inside the container via port 5000 on your host machine.

 - **Check Docker Compose File is Working Or Not**
```bash
docker compose up
docker compose down
```
**docker compose up**: Starts the application defined in the `docker-compose.yml` file.
**docker compose down**: Stops and removes the containers defined in the `docker-compose.yml` file.

- **To Commit the changes**
```bash
git add .
```
Add all file in staged form 
```bash
git commit -m "Commit with Dockerfile and Docker-Compose.yml file"
```
Commit all changes 

- **Push Code in your GitHub Repo**
```bash
git push
```
GitHub Repo get update 

## Jenkins pipeline ##
### Setup the pipeline ###
- **Open Jenkins**  : Go to your browser and search for `localhost:8080`. This is the default port to open Jenkins.

- **Crate New Pipeline**  : Click on New item -> Enter the item name -> select the Pipeline

- **Set Up Pipeline**
  - Step 1: Click on "GitHub Project" and add your project (repo) URL.
  - Step 2: In "Build Triggers" click on "GitHub hook trigger for GITScm polling."
  - Step 3: In "Pipeline" Definition is "Pipeline Script"
  - Step 4: Write the Script
```bash
pipeline{
    agent any 
    
    stages{
        stage("Clone"){
            steps{
                echo "Clone the code from github"
                git url:"https://github.com/AdityaThorat679/nodejs-demo-app.git", branch:"main"
            }
        }
        stage("Build"){
            steps{
                echo "Build the images"
                sh "docker build -t nodejs-demo-app ."
            }
        }
        stage("Run"){
            steps{
                echo "Deploy the container"
                sh "docker compose down && docker compose up"
            }
        }
    }
}
```
  - Step 5: Click on Save and Click on Build Now




  


  
  




