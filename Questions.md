Create a new pod called web-pod with image busybox.
Allow the pod to be able to set system_time
The container should sleep for 3200 seconds

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
