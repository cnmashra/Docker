# Docker Registry

Docker Registry : It is used to tag the image and then we can upload the container package with the apps to Docker hub.
follow the below steps to execute

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker login
Authenticating with existing credentials... [Username: ragh1988]

i Info → To login with a different account, run 'docker logout' followed by 'docker login'


Login Succeeded
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker images
REPOSITORY                 TAG       IMAGE ID       CREATED       SIZE
two-tier-flask-app-flask   latest    206217c69d38   9 hours ago   375MB
mysql                      latest    90ec22e21be2   2 weeks ago   939MB
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker image tag two-tier-flask-app-flask:latest ragh1988/two-tier-backend:latest 
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker images
REPOSITORY                  TAG       IMAGE ID       CREATED       SIZE
two-tier-flask-app-flask    latest    206217c69d38   9 hours ago   375MB
ragh1988/two-tier-backend   latest    206217c69d38   9 hours ago   375MB
mysql                       latest    90ec22e21be2   2 weeks ago   939MB
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % docker push ragh1988/two-tier-backend:latest
The push refers to repository [docker.io/ragh1988/two-tier-backend]
6e9d1c9aa92f: Pushed 
b7487efe6aac: Pushed 
f60737083441: Pushed 
6335fc2bd7ed: Pushed 
15675efe1a99: Pushed 
8a9d59c6c7ba: Pushed 
0d8bbfd92457: Mounted from library/python 
27e9ade6615b: Mounted from library/python 
6a77241ff1e8: Mounted from library/python 
090e9c58f474: Mounted from library/python 
latest: digest: sha256:04baf889a8aab5027e92fdb9d44a246f88ce9934d5590121673c3e5a6f7073c8 size: 2416
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/two-tier-flask-app % 




```
