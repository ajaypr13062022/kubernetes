Taint and toleration will only tell the node to accept certain tolerations.

Taint - Node

Syntax:
        $ kubectl taint nodes node-name key=value:taint-effect
            tainr-effect --> 1) NoSchedule
                             2) PreferNoSchedule
                             3) NoExecute
Example:
        $ kubectl taint nodes node1 app=blue:NoSchedule


Tolerant - Pod

pod-definition.yaml
-----------------------
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
    - name: nginx-container
      image: nginx

  tolerations:
    - key: "app"
      operator: "Equal"
      value: "blue"
      effect: "NoSchedule"
-----------------------------
