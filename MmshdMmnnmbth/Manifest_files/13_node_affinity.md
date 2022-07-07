Primary purpose is to ensure pods are placed on the particular node

pod-definition.yaml
-----------------------------------------------------
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
    - name: data-processor
      image: data-processor
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
          - matchExpressions:
             - key: size
               operator: In     # NotIn, Exists
               values:
                 - Large
                 - Medium        # Small
------------------------------------------------------

Node Affinity Types
Available:
    requiredDuringSchedulingIgnoredDuringExecution
    preferredDuringSchedulingIgnoredDuringExecution
Planned:
    requiredDuringSchedulingRequiredDuringExecution