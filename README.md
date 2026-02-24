STEP 1: Download the Frontend and backend code in your local terminal.
        GO to your github.
        Create one Repository(with public access).
        Push the code to created Repository.
        
STEP 2: Create One Server(create Public subnet for internet access)
        Open port 22 and 80 in server
        Then:
        SSH into created Server.
        
STEP 3: Install docker and docker compose on server
        sudo apt update
        sudo apt install docker.io docker-compose -y
        sudo systemctl enable docker
        sudo usermod -aG docker ubuntu
        
STEP 4: Install git on server
        Create one directory for this project
        Clone your repository inside the directory you created in server.
        
STEP 5: Go to backend directory 
        add Dockerfile for backend.
        
STEP 6: Go to frontend directory
        add Dockerfile for frontend.
        
STEP 7: Create docker-compose.yaml(includes mongodb and nginx setup) inside the current directory where backend and frontend code is present.

STEP 8: Setup nginx reverse proxy
        Nginx/default.conf
        
STEP 9: docker-compose up -d --build
        Now app run on you server IP
        ex: http://PUBLIC_IP
        
STEP 10: Docker login inside the server
         docker login -u username
         then
         enter your dockerhub password.
         
STEP 11: Tag the images
         Create Repositories for backend and frontend
         Then
         docker tag backend YOUR_DOCKERHUB/backend:latest
         docker tag frontend YOUR_DOCKERHUB/frontend:latest  
         
STEP 12: Push image to docker hub
         docker push YOUR_DOCKERHUB/backend:latest
         docker push YOUR_DOCKERHUB/frontend:latest
         NOTE:Image name should be updated in docker-compose.yaml
         
STEP 13: CI/CD with github actions

    STEP 1: Setting up Repository secrets:
         Open settings in the repository where your application(frontend and backend code) present.
         Left side bar click on secrets and variables 
         click on Actions
         Click on New repository secret
         Add secret name and value then click on add secret
         Example: Crete secrets of:
                  Name: DOCKER_PASSWORD  value: your-dockerhub-password
                  Name: DOCKER_USERNAME  value: your-dockerhub-username
                  Name: SSH_PRIVATE_KEY  value: Private-key-of-your-local-terminal
                  Name: VM_IP            value: Public-ip-of-your-server
                  How to find SSH_PRIVTAE_KEY?
                  Go to your local terminal 
                  cd .ssh
                  ls
                  check for private_key private_key.pub (Note: keyname depends on which name you have used while creating)
                  cat private_key
                  take the value and keep in SSH_PRIVATE_KEY secret
                  If there is no key create one.
                  
     STEP 2: Creating Workflow
          In the same github repository where you have created Repository secrets,
          CLICK on Actions
                   New Workflow
                   Setup workflow of yourself
                   write the workflow (Example: .github/workflows)
                   Commit changes  (Note: while commiting, commit changes to the branch where you pushed the code)


NOW THE SETUP IS COMPLETE.
WHAT IT DOES?
if Developer pushes code →
GitHub Actions builds image →
Pushes to DockerHub →
SSH into VM →
docker-compose pull →
Containers restart automatically →
App updated on port 80

Now you can access the application using the SERVER-PUBLIC-IP  (EX: http://server-public-ip)



                   
         
         
        
