## Deploying Zeppelin on kubnernetes

### Files

#### docker Directory

* Dockerfile: Zeppelin Docker image
* others: Zeppelin configure file

#### Others

* zeppelin-controller.yaml: Yaml script to create zeppelin pods on kubernetes
* zeppelin-service.yaml: Yaml script to create zeppelin service on kubernetes


### How-to-build

1. build zeppelin docker image

    ```bash
    docker build -f Dockerfile -t zeppelin:0.8.2 .
    ```

2. create `zeppelin` pod

    ```bash
    kubectl create -f zeppelin-controller.yaml
    ```
3. create `zeppelin` service
    ``` bash
    kubectl create -f zeppelin-service.yaml
    ```

4. check pods status
    ```
    kubectl get pods
    ```

5. get zeppelin service port 
    ```bash
    kubectl describe service zeppelin
    ```
