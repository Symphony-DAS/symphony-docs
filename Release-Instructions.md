# Release Instructions

Symphony does not currently have an automated release system. These release instructions have been created in order to avoid mistakes while making a release.

## Instructions

### Build the core framework
1. Pull the latest symphony-core2 repository changes and ensure everything is up-to-date by running: `git pull; git submodule foreach --recursive "(git checkout master; git pull)"; git status`
1. Open the Developer Command Prompt for VS2012
1. Change directory to the root symphony-core2 source directory containing the Build.proj file (i.e. src\symphony-core)
1. Clean and build the project by running (*replace SYMPHONY_VERSION with the next release version number*):
  `msbuild Build.proj /t:Clean,Build /p:Configuration=Release /p:Platform=x64 /p:SYMPHONY_VERSION=2.0.2.1`
1. Copy the necessary assemblies from bin/x64/Release to symphony-matlab2/lib/Core Framework:
  - HDF5.dll
  - hdf5_hldll.dll
  - hdf5dll.dll
  - HDF5DotNet.dll
  - HekaDAQInterface.dll
  - HekaIOBridge.dll
  - HekaNativeInterop.dll
  - log4net.dll
  - Symphony.Core.dll
  - Symphony.ExternalDevices.dll
  - Symphony.SimulationDAQController.dll
  - szip.dll
  - zlib.dll

### Build the app package
1. Pull the latest symphony-matlab2 repository changes and ensure everything is up-to-date by running: `git pull; git submodule foreach --recursive "(git checkout master; git pull)"; git status`
1. Open MATLAB
1. Change directory to the root symphony-matlab2 directory
1. Generate the documentation from the wiki by running: `site`
1. Replace src/main/resources/docs with target/site
1. Add the lib and src directory and their child directories to the MATLAB path
1. Open Symphony.prj
1. Click "Refresh dependencies"
1. Close the project
1. Edit `symphonyui.app.App` and make sure the version matches the next release version number (*this should generally be the same number used while building the core*)
1. Package the app by running: `package`

The releasable app (Symphony.mlappinstall) is now under the target directory.
