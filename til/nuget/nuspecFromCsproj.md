# Create nupkg from csprog

https://docs.nuget.org/create/creating-and-publishing-a-package

basically:

- nuget spec in csproj directory  
- ensure all the $replacement values are set, see table in above link  
- nuget pack the csproj.

Don’t download or install the Extension that is available with VS. That just overcomplicates things.

Download nuget.exe, that run as command line.

## Creating a Package

There are a few approaches to creating a package. Most packages are very simple and contain a single assembly. In those cases, there are some very easy ways to create packages. We’ll cover more interesting cases later.
From an assembly
If you have an assembly, you can easily generate a nuspec file from metadata within the assembly and create a package.
nuget spec MyAssembly.dll
This creates a Nuspec file. Edit the NuSpec file as needed and then
NB. If you want to have several files added to a library, make sure to use a common name.
You could manually also create the file so long as it includes the following:

```xml
<?xml version="1.0"?>
<package >
  <metadata>
    <id>How you reference the install</id>
    <version>1.0.0</version>
    <authors>Author</authors>
    <owners>UKHO</owners>    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>about the project</description>
    <releaseNotes>what the release contains</releaseNotes>
    <copyright>Copyright 2013</copyright>
    <dependencies>
    </dependencies>
  </metadata>
</package>
```

Not had to use dependencies yet, so not sure how that behaves, I would assume it allows you to include a reference to other nuget packages?
Save as xxxx.nuspec next to nuspec file create lib directory and below that a directory to represent the framework (net40 for example would do 4.0).
nuget pack MyAssembly.nuspec
From a project
For simple packages, creating a package from a csproj or vbproj file is a convenient way to create packages. For example, other packages that have been installed into your project will be referenced as dependencies when you create a package this way.
In the folder where the csproj file is, run:
nuget spec

To check if it has infact installed, you can use, from the PM console:

```powershell
Get-Package -ListAvailable -Filter UKHO.
```