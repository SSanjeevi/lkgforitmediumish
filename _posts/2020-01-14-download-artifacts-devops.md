---
toc: true
layout: post
author: "Sanjeevi Subramani"
description: Unable to download pipeline artifacts in Azure Devops Download artifacts task.
categories: [Azure Devops, Automation]
title: Unable to download pipeline artifacts in Azure Devops Download artifacts task
---

![](https://cdn-images-1.medium.com/max/2000/1*jEDk_1mMOUroYnVEcS5DGg.jpeg)

## Unable to download pipeline artifacts in Azure Devops Download artifacts task

When build artifacts are published using publish build artifacts in azure devops yaml pipeline got error that unsupported artifact type is passed when downloading with Download Artifacts task.
>  steps:
- script: ./buildSomething.sh
- task: CopyFiles@2
 inputs:
 contents: ‘_buildOutput/**’
 targetFolder: $(Build.ArtifactStagingDirectory)
- task: PublishBuildArtifacts@1
 inputs:
 pathToPublish: $(Build.ArtifactStagingDirectory)
 artifactName: MyBuildOutputsWe can’t download those artifacts using download artifacts task below.
>  steps:
- download: current
 artifact: WebApp

Because above two are different, one is pipeline artifacts and another one is build artifacts.

Below is task if you want to publish and download Build artifacts both should be used as a combination pair if the combination changed it won't work.

## Combination One:

Publish Build artifacts:
>  steps:
- script: ./buildSomething.sh
- task: CopyFiles@2
 inputs:
 contents: ‘_buildOutput/**’
 targetFolder: $(Build.ArtifactStagingDirectory)
- task: PublishBuildArtifacts@1
 inputs:
 pathToPublish: $(Build.ArtifactStagingDirectory)
 artifactName: MyBuildOutputs

Download Build artifacts
>  - task: DownloadBuildArtifacts@0
 inputs:
 buildType: ‘current’ 
 downloadType: ‘single’ 
 artifactName: MyBuildOutputs
 downloadPath: ‘$(System.ArtifactsDirectory)’

### Combination Two:
**For using pipeline artifacts for publish and download.**

Publish pipeline artifacts
>  steps:
- publish: $(System.DefaultWorkingDirectory)/bin/WebApp
 artifact: WebApp

Download pipeline artifacts
>  steps:
- download: current
 artifact: WebApp

Thanks.
