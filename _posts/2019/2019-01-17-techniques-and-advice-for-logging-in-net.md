---
title: "Techniques and Advice for Logging in .NET"
date: "2019-01-17"
---

When setting out to design maintainable software, one of the most critical things to bear in mind is creating feedback loops that allow you to make code decisions based on the application's actual use and performance under real-world circumstances. A crucial aspect of this is that your application **needs to be able to tell you when something is wrong.**

One of the main ways to achieve this is by application logging. There are many forms of logging, but in the scope of this article we will discuss a few categories of logging:

- [Diagnostic Logging](#diagnostic)
- [Performance Logging](#performance)
- [User Behavior Logging](#user)
- [Code Behavior Logging](#code)
- [Audit Logging](#audit)

[](#)

## Diagnostic Logging

Diagnostic logging is, broadly logs that help you identify and troubleshoot failure scenarios in your application. Below we will discuss a variety of ways to employ diagnostic logging to help reduce your time spent tracking down tricky bugs to help you spend more time on the fun parts of programming.

### Catchall Exception Logging

This is the most basic form of exception logging, but its great benefit is that if any code is written in your application that does not correctly handle exceptions, you are guaranteed to have a log about it! Depending on the structure of your application this may take many forms.

In ASP.NET applications, you can [define a method in your Global.asax file](https://docs.microsoft.com/en-us/aspnet/web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling#application-level-error-handling) to handle all errors that occur during processing of an HTTP request:

```
void Application_Error(object sender, EventArgs e)
```

In an application using the Owin pipeline, you can [write a simple middleware which wraps all subsequent middleware executions in a try/catch](https://stackoverflow.com/a/34493054/1504529), something like this:

```
app.Use((context, next) =>
{
  try
  {
    return next();
  }catch(Exception ex)
  {
    // Log the exception here.
  }
}
```

In .NET desktop applications, you can use the [AppDomain](https://docs.microsoft.com/en-us/dotnet/api/system.appdomain?view=netframework-4.7.2) class' UnhandledException and FirstChanceException lifecycle events to log either all exceptions or only unhandled exceptions, whichever you prefer [(note that in recent versions of .NET Core console apps this works as well!)](https://github.com/dotnet/corefx/pull/11275):

```
AppDomain.CurrentDomain.UnhandledException += (sender, args) =>
{
  var ex = args.ExceptionObject;
  // TODO: test the exception object type and log it
};
```

### Downstream Dependency Error Logging

Any time your application interacts with a downstream dependency, such as a database or another API, you should wrap the interaction in a try/catch and log any exceptions that get thrown. This is incredibly useful for determining when failures in your application are caused by bugs or outages in other people's code!

```
try
{
  myDownstreamDependency.SendRequest()
}catch(Exception ex)
{
  // Log the exception here.
}
```

Note that when doing this, you should also include as many specifics about what you were doing in your log. Things like: which API call you were making, what URL you were accessing, what arguments you passed in, which user was taking the action, etc.

### Soft Failure Logging

As we are adding logging to our application, it is important to remember that not all failures in our code result in exceptions being thrown. There are other code failures which can result in bad/missing data without ever throwing an exception. One good example of this is when you know an operation should always return a non-empty list, but the resulting list is empty. While this may not cause an exception that causes your application to be unusable, it is still a logical error which will have some known or unknown impact on your users and should be logged.[](#)

## Performance Logging

Another thing we want to know about in our application is when something causes it to run slowly. In many cases, problems or changes in our code can cause the code to begin running more slowly, which from the user's perspective is a bug!

So any operation which a user initiates which could cause a bad user experience if it were to take too long should be wrapped in some form of performance logging. A great tool for this is [the .NET Stopwatch class](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.stopwatch?view=netframework-4.7.2).

```
var stopwatch = new Stopwatch();
stopwatch.Start();
// Do something
stopwatch.Stop();
```

After calling the Stop method on our Stopwatch, then we can check its ElapsedMilliseconds or ElapsedTicks properties to check how much time has passed, and include this information in our logs.

#### HTTP Request Performance Logging

Logging the performance of all HTTP Requests is a great way to get a high-level overview of the performance of a web application. Depending on your architecture there are a few ways of doing this, but in ASP.NET applications with a Global.asax file, you can define methods to handle the ASP.NET lifecycle events for the beginning and end of handling a request:

```
private Stopwatch _stopwatch;
protected void Application_BeginRequest()
{
  _stopwatch = new Stopwatch();
  _stopwatch.Start();
}
protected void Application_EndRequest()
{
  _stopwatch.Stop();
  // TODO: log the performance here
}
```

In an Owin application (such as ASP.NET Core apps), it's even easier, you can just define a middleware near the beginning of your Owin pipeline that calls the rest of your middleware, and log the performance there:

```
app.Use((context, next) =>
{
  var stopwatch = new Stopwatch();
  stopwatch.Start();
  var result = next(); // We run all of our other middleware
  stopwatch.Stop();
  // Log the performance here.
  return result;
}
```

### Downstream Dependency Performance Logging

Once again it is very important to keep track of your downstream dependencies. Not all problems in your application originate in your code, so being able to tell when slowness in your application originates in an API or database you depend on is very important to point your troubleshooting in the right direction (and point blame in the right direction, if you have the misfortune to work for an organization which does not have [blameless postmortems](https://codeascraft.com/2012/05/22/blameless-postmortems/)...)

As with our downstream dependency error logging, we should capture as many specifics as possible about our API call/DB query in order to facilitate rapid troubleshooting of the problem.[](#)

## User Behavior Logging

It can be very useful to know how your users are actually using your application. The scope of this extends beyond just troubleshooting bugs and problems, to informing your technical priorities and even feature grooming. Below are some suggestions about useful types of user actions to log:

### Log In/Out

Whenever a user begins or ends using your application, you should log that behavior. This provides very insightful usage statistics. Additionally, when a user attempts to log in, you should record whether their login attempt succeeded or failed - this is useful for detecting brute force and DDoS attacks, or even informing your product decisions around things like password recovery or failed password lockout thresholds/durations.

### New Features

When you release a new feature, it can be very useful to log how many users are using the feature and how they are using it. This is important feedback for an Agile development process - you can't always talk to your users about how they are using your application, but you can log what they do! Combining this with error and performance logs can give you a lot of insight into whether users are having a positive experience with a new feature.

### High-Impact Features

If a particular feature in your application is known to have a significant performance impact, it can be very good to log the frequency with which users use that feature. This might be operations such as provisioning a new virtual machine, or clearing all of the cached data for their customer.[](#)

## Code Behavior Logging

Just as User Behavior Logging is useful for finding out what your users are doing, Code Behavior Logging is useful for finding out what your code is doing.

### Application Lifecycle

Logging key events in your application lifecycle can be really useful for diagnosing startup problems and crashes. In particular, one of the first things you do when your app starts is create a log with the current machine name! This not only gives you a history of when your app was started or restarted, but also lets you make sure that your logging is working!

In a .NET Core application, the easiest place to do this is right in the beginning of the Main method:

```
public static void Main(string[] args)
{
  // Write your log here!
  CreateWebHostBuilder(args).Build().Run();
}
```

For older .NET Framework WebApps (MVC/WebForms), you will instead need to do this during the Application\_Start HttpApplication lifecycle event in your Global.asax file:

```
protected void Application_Start()
{
  // Write your log here!
  // Usually startup things like dependency injection etc. go here.
}
```

 

For WPF desktop applications, the App.xaml.cs constructor or the MainWindow's constructor are good places.

Other useful lifecycle events to capture are: application shutdown, and the execution of any recurring background worker threads which may run in the background during normal operations.

### Branch Execution

This is particularly useful in legacy codebases. Sometimes you will find yourself staring at some old code and wondering "does this code even ever get hit any more?" Branch execution logs can answer this question for you - simply add a log statement in that code branch and release it to users. It won't take long before you'll have an answer to that question.

### Data Logging

When it is not clear what the actual data in your application looks like at runtime, it can be useful to log the data itself or key attributes about it. For instance, if you are doing lots of string operations in your application, it might be useful to log the length of those strings so that you know how important optimizing your string operations is. If the strings are always small, the optimization work may not be valuable enough to do. But for long strings it might warrant a higher priority.[](#)

## Audit Logging

Audit Logging is designed to give you a record of sensitive user behaviors. There are many concerns involved in audit logging - audit logs are often customer-facing and can sometimes play a role in compliance and legal matters. So it's really important to get these ones right.

### User-Facing Data Changes

Any time a user modifies data that users have access to, and that change is persisted anywhere (such as a database or filesystem) you should generate an audit log for this behavior. Be sure to log not only the data that was modified, but the user doing it, and if possible, some details about what was changed.

### Viewing Sensitive Data

While we are normally worried about auditing when users _change_ data, some data is so sensitive that even viewing it warrants an audit log entry. What data falls into this category will vary depending on your application, but good candidates are financial information, or when one user views personal data about other users.

## Conclusion

I hope that this blog has given you some good heuristics to think about when adding logging to your application. Logs are an absolutely amazing tool when it comes time to troubleshoot a bug, diagnose an outage, or provide customers with really specific and useful data about a data loss scenario. When things go wrong (and they will) logs are what helps you put on your Sherlock Holmes hat and make sure it doesn't go wrong twice!
