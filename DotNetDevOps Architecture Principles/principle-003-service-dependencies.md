---
id: principle-003-service-dependencies
title: Service to service dependency is communicated over HTTPS and without code sharing.
version: 2019-09-07
author: Poul Kjeldager Sørensen <pks@dotnetdevops.org> https://pksorensen.com
contributers:
- Poul Kjeldager Sørensen <pks@dotnetdevops.org> https://pksorensen.com
tags:
- Communication
- ServiceProvider
---

[ ] Ask Daniel if he wants to be author

# Service to service dependency is communicate over HTTPS and without code sharing

Share contracts. Do not share implementations. And by contracts, In this case, I think most of all, which contract comes over HTTP, between your services.

Based on these contracts, you will only write an implementation that fits the service you are currently working on.

And through that, you will experience greater freedom (you can change things for that particular service without affecting others or pushing out other code), and often you will also get a thinner implementation than what a reusable software package can give you.

For a service to be as autonomous as possible, let it own its implementation, even if it is identical to an existing implementation.

It is a fine rule to follow at code level, just as at an architectural level; if a service turns out to have an addiction, add that dependency directly to the service.

```cs

public class ApiController : ControllerBase
{
    public async Task<IActionResult> AskDependency([FromServices] IHttpClientFactory httpClientFactory)
    {
        var service = httpClientFactory.CreateClient("OtherService");
        var isLive = await service.GetAsync("/.well-known/live");
        return Ok();
    }
}

public class startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddHealthChecks();
        services.AddHttpClient("OtherService",
            httpclient=> {
                httpclient.BaseAddress = new Uri("https://managmeent.dotnetdevops.org");
                httpclient.DefaultRequestHeaders.Add("ApiVersion", "2019-01-01");
            });
    }
}
