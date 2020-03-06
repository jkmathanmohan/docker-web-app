CI/CD docker-web-app sample project

Step1:- Clone the git repository

# git clone https://github.com/jkmathanmohan/docker-web-app.git

Step2:- Modify the server.js file and commit it

# git status

# git add src/server.js

# git commit -m "testing the node js web app in docker"

# git push origin master

Step3:- This will trigger the build and connect to jenkins through webhook

Step4:- Build the docker image and send the to the dockerhub.com registry

Step5:- Pull the docker latest image from the dockerhub.com registry and deploy it to web server ec2 instance

Step6:- View the result web page

https://testk85.tk/
