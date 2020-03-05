# CI/CD docker-web-app sample project 

Step1:- Clone the git repository
# git clone

Step2:- Modify the server.js file and commit it
# git status
# git add src/server.js
# git commit -m "testing the node js web server in docker"
# git push origin master

Step3:- This will trigger the buld and connect to jenkins throug webhook 

Step4:- Buld the docker image and send the to the dockerhub.com registory

Step5:- Pull the docker latest image from the dockerhub.com registory and deploy it to web server ec2 instance

Step6:- View the result web page

https://testk85.tk/
