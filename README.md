# net6.0 devcontainer cannot build net6.0

Replicated on OSX  11.4 Big Sur, docker cli.

## Replication steps:

1. Open as a remote container
2. `dotnet build`

Results in an error `The "ResolvePackageAssets" task failed unexpectedly`. See build output below.

## Facts

- Uses the recommended latest LTS devcontainer image
- Switching the project to net5.0 builds successfully (see comments in `devcon_1.csproj`)
- Building locally in net6.0 (on OSX 11.4 with dotnet sdk) works fine
- The test project for vscode-dev-containers `dotnet` contains a net5.0 project - does not test for net6.0 https://github.com/microsoft/vscode-dev-containers/tree/main/containers/dotnet/test-project

## Build output:

```
vscode ➜ /workspaces/devcon_1 (master ✗) $ dotnet build
Microsoft (R) Build Engine version 17.0.0+c9eb9dd64 for .NET
Copyright (C) Microsoft Corporation. All rights reserved.

  Determining projects to restore...
  All projects are up-to-date for restore.
/usr/share/dotnet/sdk/6.0.101/Sdks/Microsoft.NET.Sdk/targets/Microsoft.PackageDependencyResolution.targets(267,5): error MSB4018: The "ResolvePackageAssets" task failed unexpectedly. [/workspaces/devcon_1/devcon_1.csproj]
/usr/share/dotnet/sdk/6.0.101/Sdks/Microsoft.NET.Sdk/targets/Microsoft.PackageDependencyResolution.targets(267,5): error MSB4018: System.OverflowException: Arithmetic operation resulted in an overflow. [/workspaces/devcon_1/devcon_1.csproj]
/usr/share/dotnet/sdk/6.0.101/Sdks/Microsoft.NET.Sdk/targets/Microsoft.PackageDependencyResolution.targets(267,5): error MSB4018:    at Microsoft.NET.Build.Tasks.ResolvePackageAssets.CacheReader.ReadItemGroup() [/workspaces/devcon_1/devcon_1.csproj]
/usr/share/dotnet/sdk/6.0.101/Sdks/Microsoft.NET.Sdk/targets/Microsoft.PackageDependencyResolution.targets(267,5): error MSB4018:    at Microsoft.NET.Build.Tasks.ResolvePackageAssets.ReadItemGroups() [/workspaces/devcon_1/devcon_1.csproj]
/usr/share/dotnet/sdk/6.0.101/Sdks/Microsoft.NET.Sdk/targets/Microsoft.PackageDependencyResolution.targets(267,5): error MSB4018:    at Microsoft.NET.Build.Tasks.ResolvePackageAssets.ExecuteCore() [/workspaces/devcon_1/devcon_1.csproj]
/usr/share/dotnet/sdk/6.0.101/Sdks/Microsoft.NET.Sdk/targets/Microsoft.PackageDependencyResolution.targets(267,5): error MSB4018:    at Microsoft.NET.Build.Tasks.TaskBase.Execute() [/workspaces/devcon_1/devcon_1.csproj]
/usr/share/dotnet/sdk/6.0.101/Sdks/Microsoft.NET.Sdk/targets/Microsoft.PackageDependencyResolution.targets(267,5): error MSB4018:    at Microsoft.Build.BackEnd.TaskExecutionHost.Microsoft.Build.BackEnd.ITaskExecutionHost.Execute() [/workspaces/devcon_1/devcon_1.csproj]
/usr/share/dotnet/sdk/6.0.101/Sdks/Microsoft.NET.Sdk/targets/Microsoft.PackageDependencyResolution.targets(267,5): error MSB4018:    at Microsoft.Build.BackEnd.TaskBuilder.ExecuteInstantiatedTask(ITaskExecutionHost taskExecutionHost, TaskLoggingContext taskLoggingContext, TaskHost taskHost, ItemBucket bucket, TaskExecutionMode howToExecuteTask) [/workspaces/devcon_1/devcon_1.csproj]

Build FAILED.

/usr/share/dotnet/sdk/6.0.101/Sdks/Microsoft.NET.Sdk/targets/Microsoft.PackageDependencyResolution.targets(267,5): error MSB4018: The "ResolvePackageAssets" task failed unexpectedly. [/workspaces/devcon_1/devcon_1.csproj]
/usr/share/dotnet/sdk/6.0.101/Sdks/Microsoft.NET.Sdk/targets/Microsoft.PackageDependencyResolution.targets(267,5): error MSB4018: System.OverflowException: Arithmetic operation resulted in an overflow. [/workspaces/devcon_1/devcon_1.csproj]
/usr/share/dotnet/sdk/6.0.101/Sdks/Microsoft.NET.Sdk/targets/Microsoft.PackageDependencyResolution.targets(267,5): error MSB4018:    at Microsoft.NET.Build.Tasks.ResolvePackageAssets.CacheReader.ReadItemGroup() [/workspaces/devcon_1/devcon_1.csproj]
/usr/share/dotnet/sdk/6.0.101/Sdks/Microsoft.NET.Sdk/targets/Microsoft.PackageDependencyResolution.targets(267,5): error MSB4018:    at Microsoft.NET.Build.Tasks.ResolvePackageAssets.ReadItemGroups() [/workspaces/devcon_1/devcon_1.csproj]
/usr/share/dotnet/sdk/6.0.101/Sdks/Microsoft.NET.Sdk/targets/Microsoft.PackageDependencyResolution.targets(267,5): error MSB4018:    at Microsoft.NET.Build.Tasks.ResolvePackageAssets.ExecuteCore() [/workspaces/devcon_1/devcon_1.csproj]
/usr/share/dotnet/sdk/6.0.101/Sdks/Microsoft.NET.Sdk/targets/Microsoft.PackageDependencyResolution.targets(267,5): error MSB4018:    at Microsoft.NET.Build.Tasks.TaskBase.Execute() [/workspaces/devcon_1/devcon_1.csproj]
/usr/share/dotnet/sdk/6.0.101/Sdks/Microsoft.NET.Sdk/targets/Microsoft.PackageDependencyResolution.targets(267,5): error MSB4018:    at Microsoft.Build.BackEnd.TaskExecutionHost.Microsoft.Build.BackEnd.ITaskExecutionHost.Execute() [/workspaces/devcon_1/devcon_1.csproj]
/usr/share/dotnet/sdk/6.0.101/Sdks/Microsoft.NET.Sdk/targets/Microsoft.PackageDependencyResolution.targets(267,5): error MSB4018:    at Microsoft.Build.BackEnd.TaskBuilder.ExecuteInstantiatedTask(ITaskExecutionHost taskExecutionHost, TaskLoggingContext taskLoggingContext, TaskHost taskHost, ItemBucket bucket, TaskExecutionMode howToExecuteTask) [/workspaces/devcon_1/devcon_1.csproj]
    0 Warning(s)
    1 Error(s)

Time Elapsed 00:00:02.06
```