Config maps are used to pass configuration data in the form of key value pairs in kubernetes.
There are two ways to create config maps
    1) Imperative way

        Syntax: $ kubectl create configmap <config-name> --from-literal=<key>=<value>

        Example: $ kubectl create configmap app-config --from-literal=APP_COLOR=blue

                $ kubectl create configmap \
                    app-config --from-literal=APP_COLOR=blue \
                               --from-literal=APP_MOD=prod
        
        If there are many configurations, single line command will get difficult. So we give them in a file.

        Syntax: $ kubectl create configmap <config-name> --from-file=<path-to-file>

        Example: $ kubectl create configmap \
                    app-config --from-file=app_config.properties


    2) Declarative way

        config-map.yaml
        --------------------
        apiVersion: v1
        kind: ConfigMap
        metadata:
          name: app-config
        data:
          APP_COLOR: blue
          APP_MODE: prod
        -------------------

        $ kubectl create -f config-map.yaml

To view the configmaps
$ kubectl get configmaps
$ kubectl describe configmaps

        

    