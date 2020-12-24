---
toc: true
layout: post
description: 
author: Sanjeevi Subramani
categories: [API Management, Azure]
title: Azure API Management deployment using Azure Devops CI-CD Pipeline using ARM templates and Yaml file
---

Here am going to cover how to automate Azure API management deployment using Azure Devops CI-CD Pipeline using the Creator tool from this [Github repo](https://github.com/Azure/azure-api-management-devops-resource-kit).

Azure API Management Devops [Creator tool](https://github.com/Azure/azure-api-management-devops-resource-kit/blob/master/src/APIM_ARMTemplate/README.md#Creator)(Open source) is an command line tool for generating ARM templates so that we can use that in the Azure Devops pipeline to deploy to Azure.

It takes an valid.yml, Swagger.json files for each api(for each version), policy.xml file for each apis, globalpolicy.xml file and Backendurls.json file for generating ARM templates with resource details of API Management.

Valid.yml file contains the api details like below:
>  apiVersionSets: #version sets of the apis
>  - id: 1
>  displayName: Api 1
>  description: api 1
>  versioningScheme: Query #query string will contain api-version with value of version
>  versionQueryName: api-version
>  apis:
>  - name: api1 # this name should be unique and this field name is the key value used in backendurl parameters file for updating the api url as a parameter json file
>  type: http
>  displayName: API 1
>  description:
>  serviceUrl: #we are parameterizing this url in backendurl parameter input json file
>  openApiSpec: './apis/api1/1.0/Swagger.json' #swagger file path
>  policy: './apis/api1/1.0/apiServicePolicy.xml' #service level policy.xml file path
>  suffix: api1
>  subscriptionRequired: true
>  isCurrent: true
>  apiVersion: apiVersion
>  Description: api 1 revision 1 apiVersionSetId: 1
>  apiRevision: 1
>  apiRevisionDescription:
>  products: sampleproduct
>  tags:
>  diagnostic:

Creator tool Parameterized values are Backend urls, Appinsights, Appinsights Instrumentation key which will change for each environments.

## Usage:
>  `dotnet tool run apim-templates create — appInsightsInstrumentationKey $(VariableAppinsightsInstrumentationKey) — appInsightsName $(VariableAppinsightsName) — configFile “./valid.yml” — backendurlconfigFile “./TemplateAndParameters/BackendUrlParameters.json”`

where VariableAppinsightsInstrumentationKey, VariableAppinsightsName are variables we can pass in pipeline variables and the valid.yml file with api definition and description details, the Backendulrparameters.json file with urls of all the apis.

Sample [valid.yml](https://github.com/SSanjeevi/APIM-Devops-Sample-Pipeline/blob/master/InputFiles/valid.yml) file

Sample [BackendUrl.json](https://github.com/SSanjeevi/APIM-Devops-Sample-Pipeline/blob/master/InputFiles/TemplateAndParameters/SampleBackendUrlParameters.json) file

Below is the sample solution structure i have used for this pipeline input :

![](https://cdn-images-1.medium.com/max/2000/1*kCY0_tSUhzIyIDpHkDwbfw.png)

Below is the sample yaml file used in Azure Devops pipeline.

![](https://cdn-images-1.medium.com/max/5152/1*cuZZ6myRIci6OhHjdyXzFg.png)

You can refer the files in this github repo:
[**SSanjeevi/APIM-Devops-Sample-Pipeline**
*You can't perform that action at this time. You signed in with another tab or window. You signed out in another tab or…*github.com](https://github.com/SSanjeevi/APIM-Devops-Sample-Pipeline)

Thanks,

Sanjeevi Subramani
