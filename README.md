# Cisco Microservices Kubernetes Demo (please view in RAW format)

Demo microservices architecture with kubernetes

Different networking options within Docker:
1) Default docker bridge via docker 0
In a host: eth0 -- IP Tables/NAT -- Docker 0 -- container 1
                                             \
                                              \ container 2
                                              
2) User defined bridges to isolate containers in the same host
In a host: eth0 -- IP Tables/NAT -- Brnet1 -- container 1
                                 \
                                  \ Brnet2 -- container 2
                                  
3) Overlay Network
In host 1: eth0 -- IP Tables/NAT -- Docker 0 -- container 1
                                                           \
                                                             \ 
                                                               overlay(for containers to talk across multi hosts without NAT)
                                                               /
                                                              /
In host 2: eth0 -- IP Tables/NAT -- Docker 0 -- container 2

Why do we need Docker?

- Faster development process
- Application encapsulation
- The same behaviour on local machine, dev, staging, production servers
- Easy and clear monitoring
- Easy to scale

To run web_server_hello via minikube:
1) Start minikube:
minikube start --vm-driver=vmfusion

2) Set docker env:
eval $(minikube docker-env)

3) Build image (go to ../b2bmicroservices/b2bhello/):
docker build -t hello_image .

4) Run in minikube:
kubectl run hello --image=hello_image --image-pull-policy=Never

5) Check that it's running:
kubectl get pods

6) Check for output via logs:
kubectl logs {pod-name}
Note: get {pod-name} from 5)


To run web_server_bye via minikube:
1) Start minikube:
minikube start --vm-driver=vmfusion

2) Set docker env:
eval $(minikube docker-env)

3) Build image (go to ../b2bmicroservices/b2bbye/):
docker build -t bye_image .

4) Run in minikube:
kubectl run bye --image=bye_image --image-pull-policy=Never

5) Check that it's running:
kubectl get pods

6) Check for output via logs:
kubectl logs {pod-name}
Note: get {pod-name} from 5)


To run web_server_hello nginx server via docker:
1) Go to ../b2bmicroservices/web_server_hello/examples/nginx

2) Execute command: docker run -it --name "test-nginx-hello" -p 8080:8080 -v $(pwd):/usr/share/nginx/html:ro nginx:latest /bin/bash

3) Inside shell, run: nginx -c /usr/share/nginx/html

4) Server is running now, go to localhost:8080/app1, and index.html will be served


To run web_server_bye nginx server via docker:
1) Go to ../b2bmicroservices/web_server_bye/examples/nginx

2) Execute command: docker run -it --name "test-nginx-bye" -p 8081:8080 -v $(pwd):/usr/share/nginx/html:ro nginx:latest /bin/bash

3) Inside shell, run: nginx -c /usr/share/nginx/html

4) Server is running now, go to localhost:8080/app2 on the web browser, and index.html will be served
