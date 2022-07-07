Secrets are used to store sensitive information, like passwords or keys. They are similar to configMaps, except that they are stored in an encoded or hashed format.

There are 2 ways to create a secret.
    1) Imperative way
        syntax:
                $ kubectl create secret generic <secret-name> --from-literal=<key>=<value>

        Example:
                $ kubectl create secret generic \
                    app-secret --from-literal=DB_HOST=mysql \
                                --from-literal=DB_User=root \
                                --from-literal=DB_Password=paswrd
        
        input from a file
        syntax:
                $ kubectl create secret generic <secret-name> --from-file=<path-to-file>

        Example:
                $ kubectl create secret generic \
                    app-secret --from-file=app_secret.prop

    2) Declarative way

        secret-data.yaml
        ------------------
        apiVersion: v1
        kind: Secret
        metadata:
          name: app-secret
        data:
          DB_Host: bXlzcWw=
          DB_User: cm9vdA==
          DB_Password: cGFzd3Jk
        ----------------------

        $ kubectl create -f secret-data.yaml

To create a encoded text or hashed text
-------------------------------------------
ajay@master:~$ echo -n 'mysql' | base64
bXlzcWw=
ajay@master:~$ echo -n 'root' | base64
cm9vdA==
ajay@master:~$ echo -n 'paswrd' | base64
cGFzd3Jk
------------------------------------------

To view the newly created secret
$ kubectl get secrets
$ kubectl describe secrets
$ kibectl get secret app-secret -o yaml

To decode the hashed text
-----------------------------------------------------
ajay@master:~$ echo -n 'bXlzcWw=' | base64 --decode
mysql
ajay@master:~$ echo -n 'cm9vdA==' | base64 --decode
root
ajay@master:~$ echo -n 'cGFzd3Jk' | base64 --decode
paswrd
-----------------------------------------------------