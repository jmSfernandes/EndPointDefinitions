# EndPointDefinitions
[![Nuget badge](https://img.shields.io/nuget/v/MinimalApi.EndPointDefinitions)](https://www.nuget.org/packages/MinimalApi.EndPointDefinitions/1.0.0)
[![Nuget badge](https://img.shields.io/nuget/dt/MinimalApi.EndPointDefinitions)](https://www.nuget.org/packages/MinimalApi.EndPointDefinitions/1.0.0)


A library to enable the easy definition of endpoints with .NET8 minimal API projects.

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

And you have full control to still define your services lifecycle.

**You can check the full example [project](https://github.com/jmSfernandes/ExampleEndpointDefinitions) to see the full implementation**.


Then you only need to call the `Services.AddAllEndpointDefinitions` or the `Services.AddEndpointDefinition(Type type)` to define the 
endpoints. 

And the `app.UseEndpointDefinitions()` to start the Endpoints.

As shown here:

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


## LICENSE 
MIT License

Copyright (c) 2022 J. Fernandes

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.




