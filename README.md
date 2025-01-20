# godot_export_script
 
I created this script to automate a lot of steps I found myself doing manually each time I wanted to export a new version of mt Godot projects. I decided to give it its own repository so that others might make some use of it, and to track iterations and improvements on it. Note that since it's a Powershell script, it can only be run in Windows (or anywhere that supports Powershell).

## What the script does

 - Creates subdirectories under an "export" directory (configurable) for the version you're exporting
 - Increments the version rev number (last number in the version string) for builds on main branch (actually updates the project.godot file)
 - For -DebugExport builds or builds on non-main branches:
   - Includes the commit SHA as part of the version in the file names
   - Doesn't update version number in project.godot
 - Exports each template to its own subdirectory, then compresses all the files to a single ZIP file
 - Has export_config.xml file to easily change settings which may differ per project (and some command-line params too)

 ## Command-line parameters

 - -DebugExport tells it to use --export-debug instead of --export-release. It also prevents version rev increase, and includes commit in version number output.
 - -NoVersionIncrement can be used to create a non-debug main branch build without increasing the version number.

## How to use

1. Copy export.ps1 and export_config.xml to your Godot project root directory (containing the project.godot)
2. Update export_config.xml to reflect your export templates that you wish to create
3. Update any other settings as necessary or desired in export_config.xml
4. Ensure your project has a version set in project.godot (or not if you don't want to use that functionality)
5. Execute export.ps1 from your Godot project root directory

## Example directory structure

For the default config exports, and default configuration options.
The zip files contain exactly the same contents as the corresponding directories.
Assuming project is "My Cool Game" with version "0.0.1":

```
My Cool Game
+-- exports
   +-- My Cool Game v0.0.1
      +-- My Cool Game v0.0.1 - Windows Desktop.zip
      +-- My Cool Game v0.0.1 - Web.zip
      +-- Windows Desktop
         +-- My Cool Game v0.0.1.exe
         +-- My Cool Game v0.0.1.pck
      +-- Web
         +-- index.html
         +-- index.js
         +-- index.pck
         +-- etc. ...
```


