# AUTOMATION in DevOps through GIT+DOC+JEN
## Project Details:-
Their would be 3 job performed:-
## JOB:1
If Developer push to dev branch then Jenkins will fetch from dev and deploy on dev-docker environment.
### JOB:2
If Developer push to master branch then Jenkins will fetch from master and deploy on master-docker environment.
both dev-docker and master-docker environment are on different docker containers.
### JOB:3
Manually the QA team will check (test) for the website running in dev-docker environment. If it is running fine then Jenkins will merge the dev branch to master branch and trigger #job 2
Now Start the automation:-
## JOB:1
1. First create git repository:-
2. Create Dev and Master Branch
![Screenshot (79)](https://user-images.githubusercontent.com/60083481/90332999-89c03e80-dfdf-11ea-9663-1bc871f8d64f.png)
--> create hook to connect gitbash to github for pull the cade by jenkins.
![hooks](https://user-images.githubusercontent.com/60083481/90334449-58e60680-dfeb-11ea-8aef-ab06ab308ef7.jpeg)

-->Configure job in jenkins to fetch from dev:-
![j1 ](https://user-images.githubusercontent.com/60083481/90334662-ee35ca80-dfec-11ea-8eeb-8af8d439e0af.jpg)

--> After that fetch dev branch in dev docker environment.
![j2](https://user-images.githubusercontent.com/60083481/90334726-584e6f80-dfed-11ea-973b-c71b0e2c107c.jpg)

Execute shell part :-
sudo cp -rvf index.html /root/devfile
if sudo docker ps | grep devenv
then
echo “already running”
else
sudo docker run -dit -p 8083:80 -v /root/devfile:/usr/local/apache2/hotdocs — name devenv httpd
fi

## JOB:2
### Configure job in jenkins to fetch from master:-
![j3](https://user-images.githubusercontent.com/60083481/90334823-fb9f8480-dfed-11ea-9843-8115227e7fa1.jpg)

![j4](https://user-images.githubusercontent.com/60083481/90335304-baa96f00-dff1-11ea-9365-1354183487ec.jpg)

Execute shell part:-sudo cp -rvf index.html /root/masterfile
if sudo docker ps | grep masterfile
then
echo “already running”
else
sudo docker run -dit -p 8085:80 -v /root/masterfile:/usr/local/apache2/hotdocs — name masterenv httpd
fi

## JOB:3
### Configure testing_job in jenkins:-
![j5](https://user-images.githubusercontent.com/60083481/90335371-3c010180-dff2-11ea-8159-58884ca32acc.jpg)

## Output
![o1](https://user-images.githubusercontent.com/60083481/90335461-d19c9100-dff2-11ea-9822-82d0f25ae235.jpg)
![o2](https://user-images.githubusercontent.com/60083481/90335491-03155c80-dff3-11ea-84cb-3e1de79d7203.jpg)
![o3](https://user-images.githubusercontent.com/60083481/90335537-453e9e00-dff3-11ea-8da1-7ee2a90c3f15.jpg)

**Yashmit Sharma** <br>

