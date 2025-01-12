# Commands

1. kubectl create -f yml file
2. kubectl edit
3. kubectl replace -f yml file
4. k replace --force -f yml file

## Namespace
1. k get ns
2. k get pods -n=nameofns
3. k run <podname> --image=redis -n=nameofns
4. k create ns/namespace nameofns

## SVC
1. k expose pod pod-name --port=port-number --name=svc-name

## Deployment
1. k create deployment deployment-name --image=img-name --replicas=nofreplica

## Expose a Pod as a service

1. k run httpd --image=httpd:alpine --port=80  <br>
Then <br>
k expose pod httpd --type=ClusterIP --target-port=80 <br>
            or <br>
 kubectl run httpd --image=httpd:alpine --port=80 --expose

## Scheduler

1. k taint node node-name key=value:taint-effect
2. **To remove the taint (impt)** : k taint nodes controlplane node-role.kubernetes.io/control-plane:NoSchedule-
3. k label node node01 color=blue

## Static Pods
1. docker ps (to view it as kubectl use api server)

2. **To find static Pod:** Run the command kubectl get pods --all-namespaces and look for those with -controlplane appended in the name










