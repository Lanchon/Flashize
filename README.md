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

`flashize <input-script> [<output-zip> [<runtime-logfile>]]`

Use `<runtime-logfile>` to create a logfile on the device during script execution.
The value of this parameter can be:
- The absolute path of the logfile to be created or appended.
- A relative path or filename to be interpreted against the path of the zipfile being run.
- A dash (-) to use the pathname of the zipfile being run with a '.log' extension.
- Null to disable logging.
