Labeling the nodes
Syntax:
    $ kubectl label nodes <node-name> <label-key>=<label-value>
Example:
    $ kubectl label nodes node-1 size=Large


pod-definition.yaml
-------------------------
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
    - name: data-processor
      image: data-processor
  nodeSelector:                 # nodeselector has limitations, so node affinity and anti-affinity are used
    size: Large
----------------------------