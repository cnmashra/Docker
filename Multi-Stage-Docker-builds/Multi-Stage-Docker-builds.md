# Multi-Stage-Docker-builds


```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % docker build -t falsk-app .
[+] Building 119.7s (10/10) FINISHED                                                                                      docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                                      0.0s
 => => transferring dockerfile: 147B                                                                                                      0.0s
 => [internal] load metadata for docker.io/library/python:3.7                                                                             3.2s
 => [auth] library/python:pull token for registry-1.docker.io                                                                             0.0s
 => [internal] load .dockerignore                                                                                                         0.0s
 => => transferring context: 2B                                                                                                           0.0s
 => [1/4] FROM docker.io/library/python:3.7@sha256:eedf63967cdb57d8214db38ce21f105003ed4e4d0358f02bedc057341bcf92a0                     112.7s
 => => resolve docker.io/library/python:3.7@sha256:eedf63967cdb57d8214db38ce21f105003ed4e4d0358f02bedc057341bcf92a0                       0.0s
 => => sha256:eedf63967cdb57d8214db38ce21f105003ed4e4d0358f02bedc057341bcf92a0 1.86kB / 1.86kB                                            0.0s
 => => sha256:eecc05bbcb03ac332705e6ce56da7536193ec685a86ded413c20d4164319a88e 2.01kB / 2.01kB                                            0.0s
 => => sha256:52801117d109624f8ecd3a9e2d6289750e01637ce7cf6764aea645ae28d6cf21 8.15kB / 8.15kB                                            0.0s
 => => sha256:796cc43785ac3cd0081892bd48e545a0615415265b60c794fdf81ac95b034213 49.59MB / 49.59MB                                         36.9s
 => => sha256:91290b4a059080b4227746016e1a8f32a290271d8712b213834e9296a38bfea9 23.57MB / 23.57MB                                         21.9s
 => => sha256:7d8d278f2f731ceff5e8c6f5010bef6b1bf18c555a80663ca612e3e42d013779 63.99MB / 63.99MB                                         34.9s
 => => sha256:c1d99d3ae80adac83c22f6fd0e8f9cdef1c9260bff794f7ca8124b639ea154cd 202.42MB / 202.42MB                                      108.4s
 => => sha256:bf433ef057e1d44230faccc25a23369730928fbf6cdb4fc794ef7486864e4fb8 6.47MB / 6.47MB                                           39.2s
 => => extracting sha256:796cc43785ac3cd0081892bd48e545a0615415265b60c794fdf81ac95b034213                                                 1.2s
 => => sha256:755c46732d51fa6d16c84bdb7ae535acb52e70029f409b553e5d9f109840ab79 14.24MB / 14.24MB                                         45.5s
 => => extracting sha256:91290b4a059080b4227746016e1a8f32a290271d8712b213834e9296a38bfea9                                                 0.3s
 => => extracting sha256:7d8d278f2f731ceff5e8c6f5010bef6b1bf18c555a80663ca612e3e42d013779                                                 1.4s
 => => sha256:669bb33af58b166a63e6aabf7cfaeb606033039c2aa3255dd32362148ed75a0f 244B / 244B                                               39.8s
 => => sha256:25ed8b4726d460a82f0be5247ed3b8f23ef8e7046cb7fb9f634f860602cf4afb 2.85MB / 2.85MB                                           42.8s
 => => extracting sha256:c1d99d3ae80adac83c22f6fd0e8f9cdef1c9260bff794f7ca8124b639ea154cd                                                 3.6s
 => => extracting sha256:bf433ef057e1d44230faccc25a23369730928fbf6cdb4fc794ef7486864e4fb8                                                 0.2s
 => => extracting sha256:755c46732d51fa6d16c84bdb7ae535acb52e70029f409b553e5d9f109840ab79                                                 0.3s
 => => extracting sha256:669bb33af58b166a63e6aabf7cfaeb606033039c2aa3255dd32362148ed75a0f                                                 0.0s
 => => extracting sha256:25ed8b4726d460a82f0be5247ed3b8f23ef8e7046cb7fb9f634f860602cf4afb                                                 0.1s
 => [internal] load build context                                                                                                         0.0s
 => => transferring context: 36.44kB                                                                                                      0.0s
 => [2/4] WORKDIR /app                                                                                                                    0.4s
 => [3/4] COPY . .                                                                                                                        0.0s
 => [4/4] RUN pip3 install -r requirements.txt                                                                                            3.2s
 => exporting to image                                                                                                                    0.1s
 => => exporting layers                                                                                                                   0.1s
 => => writing image sha256:2b5f8cccd8f74cc2293b984fc8b4d54214cab5200ba204fa11558c4802995535                                              0.0s
 => => naming to docker.io/library/falsk-app                                                                                              0.0s 
                                                                                                                                               
View build details: docker-desktop://dashboard/build/desktop-linux/desktop-linux/nqd9j46fql5w9plojzr853dtk

What's next:
    View a summary of image vulnerabilities and recommendations → docker scout quickview 
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/flask-app-ecs % 

```

<img width="1351" height="286" alt="image" src="https://github.com/user-attachments/assets/b574c33d-0ee6-4dbf-8550-6ffcc91e1eec" />
