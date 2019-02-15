## ASP.NET Core on Containers

Building a multicontainer application with nginx at front, proxying requests to a web. 
That web in turn, goes back to Nginx front to get values from a backend api.

* Frontend LB: Nginx. (image nginx which is based on busybox)
* Frontend Web: aspnetcore mvc web app (talks to the backend thru the frontend lb)
* Backend Api: aspnetcore api web app

* The web and api builds:
    * Using a linux image (alpine) with .net core sdk to build the app
    * Using another linux image (alpine) with .net core runtime to run the app 

## Starting - how to

* Since it's a multicontainer setup docker-compose is best.
    * `docker-compose up --build`
* Then go to: http://localhost:8080 for the frontend lb routing to the web
* Then go to: http://localhost:5000 for the backend api without going through frontend lb
* Then go to: http://localhost:3000 for the front web without going through frontend lb, however it will fetch values thru front lb
* You can also run the containers individually with their respective build.bat and run.bat files. Except nginx because it doesn't reach to outside it's container(s). Dunno how to fix.

## Resources

* Udemy course docker: https://www.udemy.com/docker-and-kubernetes-the-complete-guide/
* Microsoft tutorial: https://docs.microsoft.com/en-us/dotnet/core/docker/building-net-docker-images
* To override ports in aspnetcore: https://stackoverflow.com/questions/48669548/why-does-aspnet-core-start-on-port-80-from-within-docker
* Github for config aspnetcore and docker https://github.com/dotnet/dotnet-docker/blob/master/samples/aspnetapp/aspnetcore-docker-windows.md
* Github sample aspnetapp for docker https://github.com/dotnet/dotnet-docker/tree/master/samples/aspnetapp
* Combine nginx and aspnetcore https://stackoverflow.com/questions/51264577/install-nginx-on-an-existing-asp-net-core-docker-container
* Some nginx upstream examples http://nginx.org/en/docs/http/ngx_http_upstream_module.html#example
* Nginx config beginners guide: http://nginx.org/en/docs/beginners_guide.html#conf_structure
* Nginx docker images: https://hub.docker.com/_/nginx