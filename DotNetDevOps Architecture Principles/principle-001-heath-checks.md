---
id: principle-001-heath-checks
title: A services provider must provide health check endpoints
version: 2019-09-07
author: Poul Kjeldager Sørensen <pks@dotnetdevops.org> https://pksorensen.com
tags:
- DotNetCore
- Microservices
- ServiceProvider
---

# A services provider must provide health check endpoints

All service providers must provide health check endpoints at `/.well-known/ready` and `/.well-known/live` that reverse proxy/gateways can use to check the health status of the provider.

## Readiness and Liveness

* The app is functioning but not yet ready to receive requests. This state is the app's readiness.
* The app is functioning and responding to requests. This state is the app's liveness.

The readiness check usually performs a more extensive and time-consuming set of checks to determine if all of the app's subsystems and resources are available. A liveness check merely performs a quick check to determine if the app is available to process requests. After the app passes its readiness check, there's no need to burden the app further with the expensive set of readiness checks—further checks only require checking for liveness.


## Example
The basic example looks like this and further in-depth resource can be found at https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/health-checks?view=aspnetcore-2.2

```cs
public class startup
{
	public void ConfigureServices(IServiceCollection services)
	{
		services.AddHealthChecks();
	}
	public void Configure(IApplicationBuilder app, IHostingEnvironment env)
    {
        app.UseHealthChecks("/.well-known/ready", new HealthCheckOptions()
        {
            Predicate = (check) => check.Tags.Contains("ready"),
        });

        app.UseHealthChecks("/.well-known/live",new HealthCheckOptions
        {
                Predicate = (_)=>false
        });

	}
	
}
```