# EndPointDefinitions

A library to enable the easy definition of endpoints with .NET6 minimal API projects.

To use import the project from [nuget](https://www.nuget.org/packages/MinimalApi.EndPointDefinitions/1.0.0).

A full example of how to use the library is available in this [project](https://github.com/jmSfernandes/ExampleEndpointDefinitions).

## Using the library:

Defining an Endpoint:
```C#

public class WeatherEndpoint : IEndpointDefinition
{
    public void DefineServices(IServiceCollection services)
    {
        //Define services here
        services.AddScoped<IWeatherService, WeatherService>();
    }

    public void DefineEndpoints(WebApplication app)
    {
        app.MapGet("/weatherforecast", GetWeatherForecast)
            .WithName("GetWeatherForecast");
    }
...

}

```

To define an Endpoint you need to implement the `IEndpointDefinition` interface, and override both of the methods showed.
You do not need to use Services, you can define the GetWeatherForecast as a lambda or a extracted method within the Endpoint Class.
The example serves only to show that it is possible to use services and dependency injection with the library.
You can check the example [project](https://github.com/jmSfernandes/ExampleEndpointDefinitions) to see the full implementation.

Then you only need to call the `Services.AddAllEndpointDefinitions` or the `Services.AddEndpointDefinition(Type type)` to define the 
endpoints. 
And the `app.UseEndpointDefinitions()` to start the Endpoints.

```C#

builder.Services.AddAllEndpointDefinitions();

//its also possible to filter for specific endpointDefinitions
//builder.Services.AddEndpointDefinitions(typeof(WeatherEndpoint));
...

var app = builder.Build();

...

//Start Endpoint definitions
app.UseEndpointDefinitions();
app.Run();
```






