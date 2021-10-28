# Private Atronas Helm Repositry

This Helm Package doesnt run out of the box, Needs to be Configured

- Create Mysql Users :
    - CREATE USER 'name'@'%' IDENTIFIED BY 'password';
    - GRANT ALL PRIVILEGES ON *.* TO 'surt'@'%'WITH GRANT OPTION;
    - GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
    - FLUSH PRIVILEGES;
- Create a Secreate with Login Credentials to pull the images from the repo
    ```
    - kubectl create secret docker-registry SECRET_NAME  --docker-username=DOCKER_USERID --docker-password=DOCKER_PASSOWRD    --docker-email=DOCKER_EMAIL -n NAMESPACE

    - kubectl get serviceaccounts default -o yaml > ./sa.yaml -n NAMESPACE

    - EDIT imagePullSecrets:
        - name: SECRET_NAME
    - kubectl replace serviceaccount default -f ./sa.yaml -n NAMESPACE
    ```

# Important

Sap Con has to be scheduled only on one node , So Please specify value for nodeKey and nodeValue in the values.yaml

## HELPER COMMANDS
- docker exec k3d-k3s-default-server-0 sh -c "ctr image list -q | grep registry.gitlab | xargs ctr image rm"

- kubectl port-forward mysql-8d5cc4bd4-rltrg 3306:3306 --address 0.0.0.0

- kubectl port-forward <your-mysql-pod-name> 3306:3306 -n <your-namespace>

- helm template example-app atronas-app --values .\atronas-app\values.yaml



