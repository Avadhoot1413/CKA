Create a new pod called web-pod with image busybox.Allow the pod to be able to set system_time.The container should sleep for 3200 seconds

Answer-->
kubectl run web-pod --image=busybox --command sleep 3200 --dry-run=client -o yaml > busybox.yml

#busybox yaml will be generated
#add below content in yaml
securityContext:
      capabilities:
        add: ["SYS_TIME"]
		
		
controlplane $ cat busybox.yml 
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: web-pod
  name: web-pod
spec:
  containers:
  - command:
    - sleep
    - "3200"
    image: busybox
    name: web-pod
    securityContext:
      capabilities:
        add: ["SYS_TIME"]
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}

kubectl apply -f busybox.yml

==================================================================================================================================================================

Create a new deployment called myproject, with image nginx:1.16 and 1 replica. Next upgrade the deployment to version 1.17 using rolling​ update​. Make sure that the version upgrade is recorded in the resource annotation.
##Createing a new deployment called myproject, with image nginx:1.16 and 1 replica
kubectl create deployment myproject --image=nginx:1.16 
kubectl get deployment
kubectl describe deployment myproject
##upgrade the deployment to version 1.17 using rolling​ update.Make sure that the version upgrade is recorded in the resource annotation.
kubectl set image deployment/myproject nginx=nginx:1.17 --record
kubectl rollout history deployment myproject

==================================================================================================================================================================

Create a new deployment called my-deployment. Scale the deployment to 3 replicas.Make sure desired number of pod always running.
Answer -->
kubectl create deployment my-deployment --image=nginx --replicas=3

==================================================================================================================================================================

Deploy a web-nginx pod using the nginx:1.17 image with the labels set to tier=web-app
kubectl run web-nginx --image=nginx:1.17 --labels tier=web-app

==================================================================================================================================================================

