# AST Metrics Component 
![AST Metrics Component](docs/service-diagramm.png "AST Metrics Component")

# Installation Instruction

   Prerequisites : Install new cluster 
    ```
       k3d cluster create dev --k3s-arg "--disable=traefik@server:0" --port 8080:80@server:0 

    ```

1 . Install operator (contains Kubernetes CRD's custom resources : Microservice and Microfrontend)

   ```
helm upgrade operator --install --create-namespace \
--namespace default ast/operator-helm-chart \
--set config.domain=127.0.0.1 \
--set-string config.port="8080" \
--set imagePullSecretJfrog.username=user.example@checkmarx.com \
--set imagePullSecretJfrog.password=********** \
--set imagePullSecretJfrog.email=user.example@checkmarx.com
  
  ```
  
2. Install platform (contains platform services : traeffic,postgres, rabbit , redis , etc )
   
```
  git clone https://github.com/CheckmarxDev/ast-components
  cd  ast-components\helm
  helm dependency build
  cd ..\platforms
  helm upgrade ast-platforms  ./helm -i
   
  ```
3.Install Core (contains core ast services :  scan, result services and webapp)  - not must only if you require services or web app

```
   git clone https://github.com/CheckmarxDev/component-core
   cd component-core
   helm upgrade core  ./helm -i
   
```
  
 4 . Install ast-metrics component

 ```
  git clone https://github.com/CheckmarxDev/component-ast-metrics
  cd component-ast-metrics
  helm upgrade ast-metrcis-management  ./helm -i
  
 ```
  
   
  
