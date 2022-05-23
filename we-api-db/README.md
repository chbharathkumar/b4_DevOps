# 1. Deploying the DB

# Below are the Postgres deployment file with PV and PVC:
- db-persistent-volume.yaml
- db-persistent-volume-claim.yaml
- db-deployment.yaml
- db-service.yaml
# Applying changes
`$ kubectl apply -f db-persistent-volume.yaml`

`$ kubectl apply -f db-persistent-volume-claim.yaml`

`$ kubectl apply -f db-deployment.yaml`

`$ kubectl apply -f db-service.yaml`


# 2. Deploying the web application

 # Building the web application image
   - Dockerfile
  First, we build the image:
  
  Ex:
  docker build . -f Dockerfile.dev -t mydockerrepo:1234/vehicle-quotes-dev:registry (Please replace your in mydockerrepo:1234)
  
  docker push localhost:32000/vehicle-quotes-dev:registry
  
  # Web YAML Files
   - web-deployment.yaml
   - web-persistent-volume.yaml
   - web-persistent-volume-claim.yaml
   
   Note: The only notable element here is the PV’s hostPath. I have it pointing to the path where I downloaded the app’s source code from [GitHub](https://github.com/megakevin/end-point-blog-dotnet-5-web-api). Make sure to do the same on your end.
   - web-service.yaml
   
   Run the above yaml files for web api deployment
   
`$ kubectl apply -f web-persistent-volume.yaml`

`$ kubectl apply -f web-persistent-volume-claim.yaml`

`$ kubectl apply -f web-deployment.yaml`

`$ kubectl apply -f web-service.yaml`

# Starting the application

`$ kubectl exec -it pod_name -- bash`

You’ll get a prompt like this:

`vscode ➜ /app (master ✗) $`

Now it’s just a few .NET commands to get the app up and running. First, compile and download packages:

`$ dotnet build`

That will take a while. Once done, let’s build the database schema:

`$ dotnet ef database update`

And finally, run the development web server:

`$ dotnet run`

Now, navigate to http://ipaddress:30000 in your browser of choice and you should see our REST API’s Swagger UI:
![image](https://user-images.githubusercontent.com/26796194/169820090-91a61073-e99a-48be-bada-bb08b0e2848b.png)

