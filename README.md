## Flashize
### Turn Shell Scripts Into Flashable Android Recovery Zips

#### Features

- Automatically convert shell scripts to flashable zips with a single command.
- Don't mess with `ui_print` crap: standard output and error streams will work just fine.
- Displays the script exit code and reports it back to recovery.
- The script receives the path of the zip being flashed as its first parameter.
<br>(Other parameters reserved for future use.)
- Free software: uses GPL and LGPL version 3 and later licenses.
- For Linux and Un*x-like systems only: requires Bash shell.
<br>(It would be very easy to port to Windoze proprietary crapware, but I won't do it.)

#### Usage

`flashize <input-script> [<output-zip>]`
