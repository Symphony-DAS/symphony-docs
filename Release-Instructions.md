# Release Instructions

Symphony does not currently have an automated release system. These release instructions have been created in order to avoid mistakes while making a release.

## Instructions

### Build the core framework
1. Pull the latest symphony-core repository changes and ensure everything is up-to-date by running: `git pull; git submodule foreach --recursive "(git checkout master; git pull)"; git status`
1. Open the Developer Command Prompt for VS2012
1. Change directory to the root symphony-core source directory containing the Build.proj file (i.e. src\symphony-core)
1. Clean and build the project by running (*replace SYMPHONY_VERSION with the next release version number*):
  `msbuild Build.proj /t:Go /p:Configuration=Release /p:Platform=x64 /p:SYMPHONY_VERSION=2.0.2.1`
1. Copy the necessary assemblies from bin/x64/Release to symphony-matlab/lib/Core Framework:
  - HDF5.dll
  - hdf5_hldll.dll
  - hdf5dll.dll
  - HDF5DotNet.dll
  - HekaDAQInterface.dll
  - HekaIOBridge.dll
  - HekaNativeInterop.dll
  - log4net.dll
  - NIDAQInterface.dll
  - Symphony.Core.dll
  - Symphony.ExternalDevices.dll
  - Symphony.SimulationDAQController.dll
  - szip.dll
  - zlib.dll
1. Copy msvcp100.dll and msvcr100.dll from C:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\redist\x64\Microsoft.VC100.CRT to symphony-matlab/lib/Core Framework
1. Copy NationalInstruments.Common.dll and NationalInstruments.DAQmx.dll from C:\Program Files (x86)\National Instruments\MeasurementStudioVS2012\DotNET\Assemblies\Current to symphony-matlab/lib/Core Framework

### Build the app package
1. Pull the latest symphony-matlab repository changes and ensure everything is up-to-date by running: `git pull; git submodule foreach --recursive "(git checkout master; git pull)"; git status`
1. Open MATLAB
1. Change directory to the root symphony-matlab directory
1. Generate the documentation from the wiki by running: `site`
1. Replace src/main/resources/docs with target/site
1. Add the lib and src directory and their child directories to the MATLAB path
1. Open Symphony.prj
1. Click "Refresh dependencies"
1. Close the project
1. Edit `symphonyui.app.App` and make sure the version matches the next release version number (*this should generally be the same number used while building the core*)
1. Package the app by running: `package`

The releasable app (Symphony.mlappinstall) is now under the target directory.

### Create a new release on GitHub
1. Go to https://github.com/Symphony-DAS/symphony-matlab/releases
1. Click "Draft a new release"
1. Enter the tag version as the Symphony version number being release (e.g. 2.0.2.1)
1. Enter the release title in the format "SYMPHONY_VERSION (MAJOR.MINOR-DEV_STAGE.REV) x64" (e.g. 2.0.2.1 (2.0-rc1) x64). The third position of the full SYMPHONY_VERSION indicates the DEV_STAGE: 0 = alpha, 1 = beta, 2 = release candidate, 3 = release. The forth position indicates the REV.
1. Enter the release notes
1. Attach the Symphony.mlappinstall file
1. Mark the build as pre-release if the dev stage is alpha, beta, or release candidate

### Update the Symphony-DAS website
1. Pull the latest symphony-das.github.io repository changes and ensure everything is up-to-date by running: `git pull; git submodule foreach --recursive "(git checkout master; git pull)"; git status`
1. Open the \_config.yml file
1. Replace the "version" property value with the new Symphony version number
1. Commit and push the change to GitHub
