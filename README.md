# Docker tips & tricks

## Debugging .NET Docker containers locally together with existing Docker compose stack
The way we "normally" debug .NET applications is using either a locally running [IIS Express web server](https://learn.microsoft.com/en-us/iis/extensions/introduction-to-iis-express/iis-express-overview) instance (for .NET Framework) or a locally running [Kestrel web server](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/servers/kestrel?view=aspnetcore-8.0) instance. But, it is also possible do this for a .NET application with Docker support by [debugging the locally running container](https://learn.microsoft.com/en-us/visualstudio/containers/edit-and-refresh?view=vs-2022).

There is however an issue if this locally running Docker container needs to access other processes running as containers as part of a Docker compsoe stack. In this case the Docker container you are debugging won't be able to reach the other containers in the same way it would if it was part of the same stack. But there is a solution to this!

What this means is that after setting up the original Docker compose stack stack you can seamlessly switch out one or more containers to instead run using a local Dockerfile and debug them through Visual Studio. While debugging, the container has access to all other containers in the stack as expected. After you are done debugging you can switch back to having it running in the background (manually starting and stopping the container in Docker Desktop for now).
