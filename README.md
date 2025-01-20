# godot_export_script
 
I created this script to automate a lot of steps I found myself doing manually each time I wanted to export a new version of mt Godot projects. I decided to give it its own repository so that others might make some use of it, and to track iterations and improvements on it. Note that since it's a Powershell script, it can only be run in Windows (or anywhere that supports Powershell).

This is what the script can do:

 - Creates subdirectories under an "export" directory for the version you're exporting
 - Increments the version rev number (last number in the version string) for builds on main branch (actually updates the project.godot file)
 - Exports each template to its own subdirectory, then compresses all the files to a single ZIP file ready to upload to itch.io
 - For debug builds or builds on non-main branches, includes the commit SHA as part of the version in the file names
 - Has a config file to easily change settings which may differ per project (and some command-line params too)

 Command-line parameters:

 - -DebugExport tells it to use --export-debug instead of --export-release. It also prevents version rev increase, and includes commit in version number output.
 - -NoVersionIncrement can be used to create a non-debug main branch build without increasing the version number.