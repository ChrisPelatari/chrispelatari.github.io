---
  layout: post
  title: Implementing Stripe Checkout Session in ASP.NET Core Minimal API
  date: 2024-11-10
  categories: [dotnet, minimal-api, stripe]
  author: chrispelatari
  excerpt: I will walk through my implementation of a Stripe Checkout session using ASP.NET Core Minimal API. This approach leverages the simplicity and performance of minimal APIs while integrating with Stripe for payment processing. I'll cover setting up the project, configuring CORS, and implementing the Stripe Checkout session.
---

# Implementing Stripe Checkout Session in ASP.NET Core Minimal API

## Introduction

There are many, many examples of Stripe integration on the web, including videos. Here's the problem with *every single other example*: they HARD CODE values for processing payments. 😩

So, I will walk through my implementation of a Stripe Checkout session using ASP.NET Core Minimal API. This approach leverages the simplicity and performance of minimal APIs while integrating with Stripe for payment processing. I'll cover setting up the project, configuring CORS, and implementing the Stripe Checkout session.

TL;DR: The secret sauce is model binding in the API call, you must build up the dynamic cart contents from your front end.

## Prerequisites

- .NET 8 SDK
- Stripe account with API keys
- Front-end application (I used Vue.js)

## Setting up the project

Create a new ASP.NET Core Minimal API project using the following command:

```bash
dotnet new web -n StripeCheckoutSession
cd StripeCheckoutSession
```

Add the Stripe.NET NuGet package to the project:

```bash
dotnet add package Stripe.net
```

## Configure local.settings.json
Create a local.settings.json file in the root of your project to store your Stripe API key:

```json
{
  "Stripe": {
    "SecretKey": "sk_test_51"
  }
}
```

## Implementing the Stripe Checkout session

Add the following code to the `Program.cs` file:

```csharp
using Stripe;
using Stripe.Checkout;

var builder = WebApplication.CreateBuilder(args);

// Add CORS services to the DI container.
builder.Services.AddCors(options =>
{
  options.AddPolicy("AllowSpecificOrigin", builder =>
  {
    builder.WithOrigins("http://localhost:4000", "http://127.0.0.1:4000", "https://yourfrontend.com")
      .AllowAnyHeader()
      .AllowAnyMethod();
  });
});

// Add Application Insights telemetry
builder.Services.AddApplicationInsightsTelemetry();

var app = builder.Build();

app.UseCors("AllowSpecificOrigin");

StripeConfiguration.ApiKey = builder.Configuration["StripeApiKey"];

app.MapPost("/api/CreateCheckoutSession", async (List<SessionLineItemOptions> lineItems) =>
{
    var options = new SessionCreateOptions
    {
        PaymentMethodTypes = new List<string>
        {
            "cashapp",
            "card",
        },
        LineItems = lineItems,
        Mode = "payment",
        SuccessUrl = "https://example.com/success",
        CancelUrl = "https://example.com/cancel",
    };

    var service = new SessionService();
    Session session = await service.CreateAsync(options);

    return Results.Ok(session);
});

app.Run();
```

### The key here is the `MapPost` method, which accepts a list of `SessionLineItemOptions` as a parameter. This allows you to pass dynamically sized cart contents from the front end to the API. Not just a single T-shirt.

## Front-end implementation test

Pop this into a .http file in Visual Studio Code and run it with the REST Client extension:

```javascript
### Create Checkout Session
POST https://localhost:8080/api/CreateCheckoutSession
Content-Type: application/json

[
  {
    "Price": "price_1ofMany",
    "Quantity": 1
  }
]
```

You can specify lots of other properties if you would like to get more specific, but building items in the dashboard handles a lot of this for you. The above is the minimal implementation to get you started. It will work for that T-shirt if you set it up correctly in the Stripe dashboard. Building the front-end will likely change every two weeks anyways, so I leave that part up to you, dear reader.

## Explanation
- CORS Configuration: We configure CORS to allow requests from specific origins. This is crucial for enabling cross-origin requests from your frontend application.
- Stripe Configuration: We set the Stripe API key from the configuration file.
- Stripe Checkout Session: We define an endpoint /api/CreateCheckoutSession that accepts a list of SessionLineItemOptions. This endpoint creates a Stripe Checkout session and returns the session details.

## Conclusion

In this article, we implemented a Stripe Checkout session in an ASP.NET Core Minimal API project. We configured CORS, set up the Stripe API key, and created a Stripe Checkout session endpoint. This approach allows you to build a dynamic cart on the front end and pass the cart contents to the API for processing payments. I hope this helps you integrate Stripe Checkout in your ASP.NET Core Minimal API project. Happy coding! 🚀
