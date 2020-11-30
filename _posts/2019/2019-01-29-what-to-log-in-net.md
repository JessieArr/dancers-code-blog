---
title: "What to Log in .NET"
author: Shawn
date: "2019-01-29"
categories: [Programming]
tags: [Migrated]
---

In my [previous post](https://dancerscode.com/2019/01/17/techniques-and-advice-for-logging-in-net/), I discussed a lot of the _when_ of logging - when to log things in your application. So in this post I'd like to talk a little bit about _what_ to log.

Having lots of logs is certainly better than having none, but if the logs don't capture important information that allow you to make decisions about your application design, then they are not as valuable as they could be. So in this post I will discuss certain key pieces of information which can greatly enrich your logs:

  - Web Request Data
  - User Data
  - Caller Data
  - Environment Data
  - Error Data

[](#)

## Web Request Data

In a web application, it can be hugely useful to log certain information about the incoming request. The first things we want to take a look at are what was requested. See below for WebForms/MVC code snippets:

#### Protocol

If your web server serves both HTTP and HTTPS requests, you should log the protocol being used for the request. ([You do use HTTPS, right?](https://www.troyhunt.com/https-is-easy/))

#### Hostname

By logging the hostname, we can see the actual domain that was requested, including ports (if the port was specified) and the subdomain.

#### Path

This represents the actual request path - the part after the hostname and before the query string. In MVC apps, this is used for routing to the appropriate controller/view, and in WebForms apps this will be the path to the .aspx page which is rendered.

#### Query String

Because query strings are used for passing in important information, the request information is not really completed without it. **NOTE: if you are passing sensitive data via query strings, be sure not to log them!** Additionally, see [this StackExchange post](https://security.stackexchange.com/a/29600/159498) for reasons why you should not do this.

#### IP Address

This one is a common pitfall, but it's good information to have no matter what. Remember that the IP address is the request of the machine which sent the request to you, and not unique to a user. For instance, if multiple people in the same home visit your website on different computers, you will most likely see the same IP address for all of them.

To add to the complexity, if a proxy, CDN, or load balancer forwarded the request to you on behalf of a user, then this IP address may not be the user's at all. But take heart: well-behaved proxies will usually include the original IP in a header which you can retrieve. A common way of doing this is with the [X-Forwarded-For](https://www.loadbalancer.org/blog/iis-and-x-forwarded-for-header/) header. Some other services such as Cloudflare and Akamai instead use the [True-Client-IP](https://support.cloudflare.com/hc/en-us/articles/206776727-What-is-True-Client-IP-) header. Depending on your network infrastructure will determine where the actual user's IP address will be stored in the request.

#### User Agent

The User Agent is another important header to capture - it indicates the web browser and operating system that the user is using. This can be very useful when attempting to diagnose bugs that only occur on certain browsers, and can also give insight into the technologies in use by your users. At work we were shocked to find that an extremely small percentage of our users were viewing our website on Android TVs!

#### Code Example: WebForms and .NET Framework MVC

Below is an example of how to fetch all of these values in an MVC or WebForms app. In your Controller/Page, there is a Request property defined which contains lots of information about the request:

```
var hostname = Request.UserHostName;
var path = Request.Path;
var queryString = Request.QueryString;
var ip = Request.UserHostAddress;
var forwardedFor = Request.Headers["X-Forwarded-For"];
var trueClientIp = Request.Headers["True-Client-IP"];
var userAgent = Request.UserAgent;
```

#### Code Example: .NET Core MVC

The implementation of the MVC Controller's Request property's class is a little different in .NET Core, but the same principles still apply here:

```
var hostname = Request.Host;
var path = Request.Path;
var queryString = Request.QueryString;
var ip = Request.HttpContext.Connection.RemoteIpAddress;
var forwardedFor = Request.Headers["X-Forwarded-For"];
var trueClientIp = Request.Headers["True-Client-IP"];
var userAgent = Request.Headers["User-Agent"];
```

#### Code Example: ASP.NET Core Owin

If you need to retrieve the request data from the Owin context during the execution of your Owin pipeline (this is a great place for performance and error logging!) then it is very similar to the above example, except that we will get the request object from the Owin context instead of a property on our Controller:

```
app.Use(async (context, next) =>
{
  var hostname = context.Request.Host;
  var path = context.Request.Path;
  var queryString = context.Request.QueryString;
  var ip = context.Request.HttpContext.Connection.RemoteIpAddress;
  var forwardedFor = context.Request.Headers["X-Forwarded-For"];
  var trueClientIp = context.Request.Headers["True-Client-IP"];
  var userAgent = context.Request.Headers["User-Agent"];
  return await next();
}
```

[](#)

## User Data

It is very useful to have information about the user themselves when looking at logs. This lets you know who caused the log, but can also be a useful aid when troubleshooting bugs, since you can create a test account with similar data. It is also very useful for audit logging, if you need to answer a question about which user took an action and when.

To get data about the current user, you will need access to the user's [Principal](https://docs.microsoft.com/en-us/dotnet/api/system.security.principal.iprincipal?view=netframework-4.7.2). How you get access to this will vary by environment:

- In WebForms or .NET Framework MVC apps, the Page/Controller has a User property which will contain the current user's Principal.
- In most .NET Framework apps, you can also access the current user's Principal using [Thread.CurrentPrincipal](https://docs.microsoft.com/en-us/dotnet/api/system.threading.thread.currentprincipal?view=netframework-4.7.2).
- In .NET Core apps, [Thread.Current principal is not available](https://davidpine.net/blog/principal-architecture-changes/), and you should instead use .NET Core's dependency injection and the IHttpContextAccessor interface.
- In the Owin pipeline, you can access the User property of the HttpContext, which contains a ClaimsPrincipal.

Once you have access to the user's principal, you can use it to check whether they are properly authenticated, and get their name:

```
var userPrincipal = Thread.CurrentPrincipal;
var isAuthenticated = userPrincipal.Identity.IsAuthenticated;
var userName = userPrincipal.Identity.Name;
```

Additionally, a very common implementation of the IPrincipal interface is the [ClaimsPrincipal](https://docs.microsoft.com/en-us/dotnet/api/system.security.claims.claimsprincipal?view=netframework-4.7.2), which can contain all sorts of information about the current user - common and useful claims to look at are the user's roles, email, and any application-specific claims you might generate during user login, such as a user ID or customer ID.[](#)

## Caller Data

A very useful diagnostic tool that I've come to love is: including the file and method which actually wrote the log. While you can rely on stack traces in the case of exception logging, it can also be useful to find out where other types of logs, such as user behavior logs are being generated, in order to put them into context.

C# exposes a couple of really handy attributes for this purpose which can be applied to your method parameters. The first is the [CallerMemberNameAttribute](https://docs.microsoft.com/en-us/dotnet/api/system.runtime.compilerservices.callermembernameattribute?view=netframework-4.7.2) which contains the method name of the method which called yours. The second is the [CallerFilePathAttribute](https://docs.microsoft.com/en-us/dotnet/api/system.runtime.compilerservices.callerfilepathattribute?view=netframework-4.7.2), which contains the path on disk to the source file in which the calling class is defined (note that the path will usually correspond to the machine which compiled the code and not necessarily the one on which it is running!)

To use these attributes, you simply need to add them to nullable string parameters on your method which does the logging:

```
private void CallerExample([CallerMemberName] string memberName = null,
    [CallerFilePath] string filePath = null)
{
  var fileName = filePath.Substring(filePath.LastIndexOf(Path.DirectorySeparatorChar) + 1);
}
```

Bear in mind that the values at runtime will be the calling method - even if you use some private helper methods to do logging, in which case the method and file name may always point to your logging class. In this case, simply add the parameters with the Caller attributes to your public method and pass the values in to your private method - the values you pass in as arguments will be used instead of the actual caller values.[](#)

## Environment Data

Capturing information about the environment your code is running in can be very useful when diagnosing environmental issues, such as when an error only occurs on one server for some reason.

Some of the most useful pieces of information here are:

- Machine Name (useful to know if something is only happening on one machine.)
- Thread ID (useful for diagnosing race conditions.)
- UserAccount under which the application is running (useful for diagnosing permissions issues.)

These values can be accessed on the Environment static class:

```
var machineName = Environment.MachineName;
var threadId = Environment.CurrentManagedThreadId;
var userAccount = Environment.UserName;
```

[](#)

## Error Data

This one is fairly easy, but is nonetheless very important. Whenever your application detects an error or exception, you should log the Exception message and stack trace for diagnostics.

Many programmers simply log the exception itself and think that they're done, but remember - your exception logs will be the first place you look when diagnosing a bug! Think ahead and put yourself in your shoes and consider what additional information might help you get to the bottom of a tricky bug, and log it now! Good candidates for this are things like method parameters, collection sizes, or user roles if an authorization exception is possible.

## Conclusion

I hope that this has given you some useful ideas and code examples to really up your logging game. As you enrich your logging story by adding additional data to logs, and a more thorough system of logging to your application, you will find yourself learning about all sorts of things that happen during your program's execution that you may never have discovered through normal testing.
