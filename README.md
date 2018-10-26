# Build.NoPackagesConfig
[![NuGet](https://img.shields.io/nuget/v/Build.NoPackagesConfig.svg)](https://www.nuget.org/packages/Build.NoPackagesConfig)
 [![NuGet](https://img.shields.io/nuget/dt/Build.NoPackagesConfig.svg)](https://www.nuget.org/packages/Build.NoPackagesConfig)

The MSBuild project SDK is used to make sure the PackageReference is used instead of packages.config.

## Purpose
The repository may content a lot of projects and solutions. You want to make sure all projects are used [PackageReference](https://docs.microsoft.com/en-us/nuget/consume-packages/package-references-in-project-files) format to manage NuGet dependencies, e.g. to use restore via MSBuild or manage NuGet dependencies in one place, etc.

The `Build.NoPackagesConfig` SDK is pretty simple. If a project includes `packages.config` file it fails the build.

## How to use
The best choose is add `Import` directive into [Directory.Build.targets](https://docs.microsoft.com/en-us/visualstudio/msbuild/customize-your-build?view=vs-2017#directorybuildprops-and-directorybuildtargets). It allows you import the SDK\`s targets into all existing project files under scope of the `Directory.Build.targets`.

**Directory.Build.targets**
```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Import Project="Sdk.targets" Sdk="Build.NoPackagesConfig" Version="1.0.0" />
</Project>
```

If you want to skip checking for a particular project you may add `SkipPackagesConfigUsageChecking` property to the project.

**SampleProject.csproj**
```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  ...
  <PropertyGroup>
    <SkipPackagesConfigUsageChecking>true</SkipPackagesConfigUsageChecking>
  </PropertyGroup>
  ...
</Project>
```
