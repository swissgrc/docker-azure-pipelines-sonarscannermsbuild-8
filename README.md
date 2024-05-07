# Docker image for running Sonar Scanner for .NET 8 in an Azure Pipelines container job

<!-- markdownlint-disable MD013 -->
[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](https://github.com/swissgrc/docker-azure-pipelines-sonarscannermsbuild-8/blob/main/LICENSE) [![Build](https://img.shields.io/github/actions/workflow/status/swissgrc/docker-azure-pipelines-sonarscannermsbuild-8/publish.yml?branch=develop&style=flat-square)](https://github.com/swissgrc/docker-azure-pipelines-sonarscannermsbuild-8/actions/workflows/publish.yml) [![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=swissgrc_docker-azure-pipelines-sonarscannermsbuild-8&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=swissgrc_docker-azure-pipelines-sonarscannermsbuild-8) [![Pulls](https://img.shields.io/docker/pulls/swissgrc/azure-pipelines-sonarscannermsbuild.svg?style=flat-square)](https://hub.docker.com/r/swissgrc/azure-pipelines-sonarscannermsbuild) [![Stars](https://img.shields.io/docker/stars/swissgrc/azure-pipelines-sonarscannermsbuild.svg?style=flat-square)](https://hub.docker.com/r/swissgrc/azure-pipelines-sonarscannermsbuild)
<!-- markdownlint-restore -->

Docker image to run [Sonar Scanner for .NET] in [Azure Pipelines container jobs].

## Usage

This image can be used to run Sonar Scanner CLI in [Azure Pipelines container jobs].

### Azure Pipelines Container Job

To use the image in an Azure Pipelines Container Job, add one of the following example tasks and use it with the `container` property.

The following example shows the container used for a deployment step which shows .NET version:

```yaml
  - stage: Build
    jobs:
    - job: Build
      steps:
      - task: SonarCloudPrepare@1
        displayName: 'Prepare analysis configuration'
        target: swissgrc/azure-pipelines-sonarscannermsbuild:8-unstable
        inputs:
          SonarCloud: 'SonarCloud'
          organization: 'myOrganization'
          scannerMode: 'MSBuild'
          projectKey: 'my-project'
          projectName: 'MyProject'
      - bash: |
          dotnet build
        displayName: "Build"
        target: swissgrc/azure-pipelines-sonarscannermsbuild:8-unstable
      - task: SonarCloudAnalyze@1
        displayName: 'Run SonarCloud analysis'
        target: swissgrc/azure-pipelines-sonarscannermsbuild:8-unstable
```

### Tags

| Tag          | Description                                     | Base Image                                 | .NET SDK | NodeJS  | Git        | Git LFS | Size                                                                                                                                           |
|--------------|-------------------------------------------------|--------------------------------------------|----------|---------|------------|---------|------------------------------------------------------------------------------------------------------------------------------------------------|
| 8-unstable   | Latest unstable release (from `develop` branch) | swissgrc/azure-pipelines-openjdk:17.0.11.0 | 8.0.204  | 20.13.0 | 2.39.2-1.1 | 3.5.1   | ![Docker Image Size (tag)](https://img.shields.io/docker/image-size/swissgrc/azure-pipelines-sonarscannermsbuild/8-unstable?style=flat-square) |

[Sonar Scanner for .NET]: https://docs.sonarqube.org/latest/analysis/scan/sonarscanner-for-msbuild/
[Azure Pipelines container jobs]: https://docs.microsoft.com/en-us/azure/devops/pipelines/process/container-phases
