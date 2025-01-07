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

1. k run httpd --image=httpd:alpine --port=80  <p>
Then <p>
k expose pod httpd --type=ClusterIP --target-port=80 <p>
            or <p>
1. kubectl run httpd --image=httpd:alpine --port=80 --expose







