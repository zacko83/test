# How to create a NuGet package

Creating your own NuGet package is extremely easy:

Add a [nuspec](https://docs.nuget.org/create/nuspec-reference) file (`<ProjectName>.nuspec`) to your project , e.g.:
```xml
<?xml version="1.0"?>
<package>
	<metadata>
		<id>$id$</id>
		<version>$version$</version>
		<authors>$author$</authors>
		<owners>$author$</owners>
		<description>$description$</description>
		<copyright>$copyright$</copyright>
	</metadata>
</package>
```

The variables within that file correspond to the values specified within `AssemblyInfo.cs`:

```cs
[assembly: AssemblyTitle("HDE.YourProject")]
[assembly: AssemblyDescription("Provides YourProject components tailored to HDE")]
[assembly: AssemblyCompany("HOTEL DE")]
[assembly: AssemblyProduct("HDE.YourProject")]
[assembly: AssemblyCopyright("Copyright © HOTEL DE 2016")]
[assembly: AssemblyVersion("2.0")]
[assembly: AssemblyFileVersion("2.0.9")]
[assembly: AssemblyInformationalVersion("2.0.9")]
```

To build the package manually, just run `nuget.exe` against the project:

```cs
nuget pack HDE.YourProject.csproj
```

In order to automate this step, add `BuildPackage` to the `csproj` file:

```xml
<PropertyGroup>
	<Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
	<Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
	<ProjectGuid>{1EC90228-A548-47BE-B7DF-EC1A34CE0990}</ProjectGuid>
	<OutputType>Library</OutputType>
	<AppDesignerFolder>Properties</AppDesignerFolder>
	<RootNamespace>HDE.YourProject</RootNamespace>
	<AssemblyName>HDE.YourProject</AssemblyName>
	<TargetFrameworkVersion>v4.5</TargetFrameworkVersion>
	<FileAlignment>512</FileAlignment>
	<BuildPackage>true</BuildPackage>
</PropertyGroup>
```

The output folder should now contain two package files `<YourProject>.<Version>.nupkg` and `<YourProject>.<Version>.symbols.nupkg`. The symbols package can be very useful for debugging (step into source must be enabled). As soon as you copied the files to our [share](\\office.hotel.de\files\ITSD\DevComponents\), it can be installed by other projects.

**Note**: You should always build your project in 'Release' mode, which will result in an optimized assembly.
