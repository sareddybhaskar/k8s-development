​ https://cloud.garr.it/support/kb/kubernetes/nodes_not_ready/
### file for creating the nodegroup and spot and ondemand instances

apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig
 
metadata:
name: EKS-course-cluster
region: us-east-1
 
nodeGroups:
  - name: ng-1
instanceType: t2.small
desiredCapacity: 3
ssh: # use existing EC2 key
publicKeyName: eks-course
  - name: ng-mixed
minSize: 3
maxSize: 5
instancesDistribution:
maxPrice: 0.2
instanceTypes: ["t2.small", "t3.small"]
onDemandBaseCapacity: 0
onDemandPercentageAboveBaseCapacity: 50
ssh: 
publicKeyName: eks-course

    

​ eksctl create nodegroup --config-file=eks-course.yaml --include='ng-mixed'


​ eksctl delete nodegroup --config-file=eks-course.yaml --include=ng-mixed --approve


​ https://automate.workativ.com/
​ eksctl scale nodegroup --cluster=EKS-course-cluster --nodes=5 --name=ng-1


​ https://kubernetes.io/docs/reference/access-authn-authz/rbac/


kind: Role
apiVersion: rbac.authorization.k8s.io/v1beta1
metadata:
  namespace: auto
  name: prod-viewer-role
rules:
- apiGroups: ["", "extensions", "apps"]
  resources: ["*"]  # can be further limited, e.g. ["deployments", "replicasets", "pods"]
  verbs: ["get", "list", "watch"] 




​ adding identity "arn:aws:iam::53:role/eksctl-preprod-nodegroup-spot-in-NodeInstanceRole-Z7RLACEPMG17" to auth ConfigMap
