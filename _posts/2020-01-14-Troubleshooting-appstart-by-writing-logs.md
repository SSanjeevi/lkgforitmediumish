---
toc: true
layout: post
author: "Sanjeevi Subramani"
description: 
categories: [DotnetCore, Troubleshooting]
title: Troubleshooting by writing logs at the application start for .NET core app using Serilog
---

![](https://cdn-images-1.medium.com/max/2000/1*-xYp4lT93KUu1teArXv5-w.jpeg)

.NET core 3.1 app may fail to start, and any logging integration implemented in startup using a middleware or anything wont log the errors for the exception occurring at the app start.

To troubleshoot this, we will write log at the Program.cs and startup.cs using Serilog.

Install Serilog related items from Nuget:
>  <PackageReference Include=”Serilog” Version=”2.10.0" />
 <PackageReference Include=”Serilog.AspNetCore” Version=”3.4.0" />
 <PackageReference Include=”Serilog.Sinks.File” Version=”4.1.0" />

Initialize the Serilog using below hightlighted code in Main method in Program.cs.

And call UseSerilog() method when setting up the HostBuilder.

Thats all we must do for setting up the Serilog for logging at app start up logs. Now you can call the Log.Error or Log.Information from the application it will log it in the file and in console if application called from console. If deployed in Azure App Service this log will come in the LogStream option also.

For App Service log at console feature in Azure App Service refer [this article](https://medium.com/lkg-in-it/troubleshooting-http-error-500-30-79e3b4f660ee).
>  namespace SampleStartupLog
{
 using System;
 using Serilog;
>  public class Program
 {
 public static void Main(string[] args)
 {
 **
Log.Logger = new LoggerConfiguration()
 .WriteTo.File(
 @”D:\home\LogFiles\Application\myapp.txt”,
 fileSizeLimitBytes: 1_000_000,
 rollOnFileSizeLimit: true,
 shared: true,
 flushToDiskInterval: TimeSpan.FromSeconds(1))
 .WriteTo.Console()
 .CreateLogger();**
>  try
 {
 CreateHostBuilder(args).Build().Run();
 }
 catch (Exception ex)
 {
 Log.Error(ex.Message + ex.StackTrace);
 }
 finally
 {
 Log.CloseAndFlush();
 }
 }
>  public static IHostBuilder CreateHostBuilder(string[] args) =>
 Host.CreateDefaultBuilder(args)
 **.UseSerilog()**
 .ConfigureAppConfiguration((hostContext, config) =>
 {
 var env = hostContext.HostingEnvironment;
>  config.SetBasePath(env?.ContentRootPath)
 .AddEnvironmentVariables();
 })
 .ConfigureWebHostDefaults(webHostBuilder =>
 {
 HostBuilderService hostBuilderService = new HostBuilderService(webHostBuilder);
 webHostBuilder.UseStartup<Startup>();
 })
 .UseDefaultServiceProvider((context, options) =>
 {
 options.ValidateScopes = context.HostingEnvironment.IsDevelopment();
 options.ValidateOnBuild = true;
 });
 }
}

Thanks.
