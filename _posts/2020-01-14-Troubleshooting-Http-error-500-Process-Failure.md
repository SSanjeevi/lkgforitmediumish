---
toc: true
layout: post
description: 
author: "Sanjeevi Subramani"
categories: [DotnetCore, Troubleshooting]
title: Troubleshooting HTTP Error 500.30 — ANCM In-Process Start Failure for .NET core App deployed in Azure App service using logging
---

In .NET Core 3.1 created a simple api and published in Azure App Service which was giving the following error: HTTP Error 500.30 — ANCM In-Process Start Failure.

I have enabled logging using Azure Application Insights but still I didn't get any logs in Application Insights for this failure.

The reason is the api is not started itself as per below description in [Microsoft portal](https://docs.microsoft.com/en-us/aspnet/core/test/troubleshoot-azure-iis?view=aspnetcore-3.1#50030-in-process-startup-failure):

The worker process fails. The app doesn’t start.

The [ASP.NET Core Module](https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/aspnet-core-module?view=aspnetcore-3.1) attempts to start the .NET Core CLR in-process, but it fails to start. The cause of a process startup failure can usually be determined from entries in the Application Event Log and the ASP.NET Core Module stdout log.

Common failure conditions:

* The app is misconfigured due to targeting a version of the ASP.NET Core shared framework that isn’t present. Check which versions of the ASP.NET Core shared framework are installed on the target machine.

* Using Azure Key Vault, lack of permissions to the Key Vault. Check the access policies in the targeted Key Vault to ensure that the correct permissions are granted.

We are not getting the configured Application insights logging because the app itself is not started and the configuration of app insights is not initiated.

To see what's failing on the startup on the app service we don't need to write or integrate any other logging components just the **Console log** using console.writeline is sufficient for logging the error on the startup.cs or program.cs like below:
>  **Program.cs**
>  public class Program
 {
 public static void Main(string[] args)
 {
 try
 {
 CreateHostBuilder(args).Build().Run();
 }
 catch (Exception ex)
 {
 Console.WriteLine(ex.Message + ex.StackTrace);
 }
 }
>  **Startup.cs**
>  public Startup(IConfiguration configuration)
 {
 try
 {
 this.Configuration = configuration;
 }
 catch (Exception ex)
 {
 Console.WriteLine(ex.Message + ex.StackTrace);
 }
 }

Now we have a question where to see this log after deploying to the Azure App Service — In Azure App service there is an Console under where you have to initiate your application as an exe like below:
>  yourapplicationName.exe

sample image shown below:

![](https://cdn-images-1.medium.com/max/3754/1*XIltjrO4HPSX621O9cXNuQ.png)

You will get the logs in the above console, so that you can see it and fix it.
>  Refer [this article for writing log using Serilog at app start into a file or console or both](https://medium.com/@ssanjeevi.ss/troubleshooting-by-writing-logs-at-the-application-start-for-net-core-app-using-serilog-14a1914701af).

Happy Coding :)

Thanks,

Sanjeevi Subramani
