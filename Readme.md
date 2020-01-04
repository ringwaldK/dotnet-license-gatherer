# LicenseGatherer

[![Build Status](https://manne.visualstudio.com/public/_apis/build/status/manne.dotnet-license-gatherer?branchName=master)](https://manne.visualstudio.com/public/_build/latest?definitionId=1&branchName=master) [![Nuget](https://img.shields.io/nuget/v/LicenseGatherer?style=flat-square)](https://www.nuget.org/packages/LicenseGatherer/) [![GitHub License](https://img.shields.io/github/license/manne/dotnet-license-gatherer.svg?style=flat-square)](https://github.com/manne/dotnet-license-gatherer/blob/master/LICENSE.txt)

> LicenseGatherer provides license information from all transitive NuGet dependencies of your solution.

## Limitation

This tool only gathers licenses from projects using the project SDK.

## Installation

As **global** tool

```batch
dotnet tool install --global LicenseGatherer
```

As **local** tool

```batch
dotnet tool install LicenseGatherer
```

## Usage

```text
Usage: LicenseGatherer [options]

Options:
  -p|--path <PATH_TO_PROJECT_OR_SOLUTION>  The path of the project or solution to gather the licenses. A directory can be specified, the value
                                           must end with \, then for a solution in the working directory is searched. (optional)
  -o|--outputpath <OUTPUT_PATH>            The path of the JSON content output. If the no value is specified some information is printed into
                                           the console. (optional)
  -s|--skipdownload                        Skip the download of licenses
  -?|-h|--help                             Show help information
```

### JSON Output

The generated JSON file consists of the following schema:

An array of **package**s.
One package has these properties

| Name                                  | Type   | Explanation                                                                          |
|---------------------------------------|--------|--------------------------------------------------------------------------------------|
| [PackageReference](#packagereference) | object | An object containing information of the package                                      |
| LicenseContent                        | string | The content of the license                                                           |
| OriginalLicenseLocation               | string | The url of the given license.                                                        |
| DownloadedLicenseLocation             | string | The corrected url of the license. E.g. It replaces the github url with the raw once. |

#### PackageReference

| Name                                | Type   | Explanation                                                                      |
|-------------------------------------|--------|----------------------------------------------------------------------------------|
| Name                                | string | The name of the package dependency                                               |
| [ResolvedVersion](#resolvedversion) | object | The runtime version. This value can differ from the version in the configuration |

#### ResolvedVersion

Contains an object of the type [NuGet.Versioning.NuGetVersion](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Versioning/NuGetVersion.cs).

## License

Licensed under [MIT](LICENSE.txt)
