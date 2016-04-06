## Flashize
### Turn Shell Scripts Into Flashable Android Recovery Zips

#### Features

- Automatically convert shell scripts to flashable zips with a single command.
- Don't mess with `ui_print` crap: standard output and error streams will work just fine.
- Can add binaries to or otherwise alter the runtime environment offered by the recovery.
- Flip Toybox the bird: includes ready-to-go Busybox binaries for various architectures.
<br>(Binaries borrowed from [busybox.net] (https://www.busybox.net).)
- Can automatically extract resources from the zipfile before invoking the script.
- Can automatically create a logfile of the output of the script.
- Displays (and possibly logs) the script exit code and reports it back to recovery.
- The script receives the path of the zipfile being flashed as its first parameter.
<br>(Other parameters reserved for future use.)
- Supports various debugging modes for runtime script tracing.
- Flashize requires Bash shell. It is developed and tested under Linux.
- Flashize is free software published under GPL and LGPL version 3 and later licenses.

<br>

#### Usage: FLASHIZE

Flashize (2016-04-06)

Converts a shell script to a flashable Android recovery zip.

`flashize <input-script> [<output-zip> [<runtime-logfile>]]`

Reads the script from standard input if `<input-script>` is a dash (-).

Names the output zipfile based on `<input-script>` if `<output-zip>` is null or a dash.

Can create a logfile on the device at runtime, according to the value of `<runtime-logfile>`:
- The absolute path of the logfile to be created.
- A relative path or filename to be interpreted against the path of the zipfile being run.
- A colon (:) to use the pathname of the zipfile being run with a '.log' extension.
- Null or a dash to disable logging.

This setting can be overridden by creating a '/tmp/flashize-log' file on the target device:
- If the file is empty then enable logging to '/tmp/flashize.log'.
- Otherwise override the value of `<runtime-logfile>` with the contents of the file.

Script debugging modes are enabled by creating dummy files on the target device:
- Create '/tmp/flashize-debug' to trace the user-supplied script.

<br>

#### Usage: FLASHIZE-EXT

Flashize-Ext (2016-04-06)

Converts a shell script to a flashable Android recovery zip. The resulting flashable zip
automatically extracts the full content of the zipfile before invoking the script.
This tool is compatible with Busybox and Toybox.

`flashize-ext <input-script> [<input-zip> [<output-zip> [<runtime-logfile> [<dest-dir>]]]]`

Reads the script from standard input if `<input-script>` is a dash (-).

Names the output zipfile based on `<input-script>` if `<output-zip>` is null or a dash.

Can create a logfile on the device at runtime, according to the value of `<runtime-logfile>`:
- The absolute path of the logfile to be created.
- A relative path or filename to be interpreted against the path of the zipfile being run.
- A colon (:) to use the pathname of the zipfile being run with a '.log' extension.
- Null or a dash to disable logging.

This setting can be overridden by creating a '/tmp/flashize-log' file on the target device:
- If the file is empty then enable logging to '/tmp/flashize.log'.
- Otherwise override the value of `<runtime-logfile>` with the contents of the file.

Extracts files to `<dest-dir>` or to '/tmp/flashize' if `<dest-dir>` is null or a dash.

Script debugging modes are enabled by creating dummy files on the target device:
- Create '/tmp/flashize-ext-debug' to trace the user-supplied script.
- Create '/tmp/flashize-debug' to trace file extraction.

<br>

#### Usage: FLASHIZE-EBB

Flashize-EBB (2016-04-06)

Converts a shell script to a flashable Android recovery zip. The resulting flashable zip
can automatically extract resources bundled within the zipfile before invoking the script.
This tool is incompatible with Toybox due to shortcomings of its 'unzip' command, and
requires Busybox instead. Thus the Toybox-based CyanogenMod 13 recovery is not supported.

`flashize-ebb <input-script> <input-zip> <output-zip> <runtime-logfile> <src-dir> <dest-dir> [<extra-src-spec>...]`

Reads the script from standard input if `<input-script>` is a dash (-).

Names the output zipfile based on `<input-script>` if `<output-zip>` is null or a dash.

Can create a logfile on the device at runtime, according to the value of `<runtime-logfile>`:
- The absolute path of the logfile to be created.
- A relative path or filename to be interpreted against the path of the zipfile being run.
- A colon (:) to use the pathname of the zipfile being run with a '.log' extension.
- Null or a dash to disable logging.

This setting can be overridden by creating a '/tmp/flashize-log' file on the target device:
- If the file is empty then enable logging to '/tmp/flashize.log'.
- Otherwise override the value of `<runtime-logfile>` with the contents of the file.

Extracts files from the zip at runtime, according to the value of `<src-dir>`:
- Null or a dash: changes to `<dest-dir>` and extracts files matching `<extra-src-spec>` there.
- A path within the zip: changes to `<dest-dir>`/`<src-dir>`, wipes its contents and extracts
  `<src-dir>` there. Also extracts files matching `<extra-src-spec>` to `<dest-dir>`.

Script debugging modes are enabled by creating dummy files on the target device:
- Create '/tmp/flashize-ebb-debug' to trace the user-supplied script.
- Create '/tmp/flashize-debug' to trace resource extraction.

<br>

#### Usage: FLASHIZE-ENV

Flashize-Env (2016-04-06)

Converts a shell script to a flashable Android recovery zip. The resulting flashable zip
can temporarily add binaries to or otherwise alter the runtime environment offered by the
recovery before invoking the script.

`flashize-env <input-script> [<env-spec> [<output-zip> [<runtime-logfile>]]]`

Reads the script from standard input if `<input-script>` is a dash (-).

Can temporarily alter the runtime environment, according to the value of `<env-spec>`:
- The name (without extension) of a configuration provided in Flashize's 'env' directory.
- The path of a user-provided zipfile containing the environment configuration.

Names the output zipfile based on `<input-script>` if `<output-zip>` is null or a dash.

Can create a logfile on the device at runtime, according to the value of `<runtime-logfile>`:
- The absolute path of the logfile to be created.
- A relative path or filename to be interpreted against the path of the zipfile being run.
- A colon (:) to use the pathname of the zipfile being run with a '.log' extension.
- Null or a dash to disable logging.

This setting can be overridden by creating a '/tmp/flashize-log' file on the target device:
- If the file is empty then enable logging to '/tmp/flashize.log'.
- Otherwise override the value of `<runtime-logfile>` with the contents of the file.

Script debugging modes are enabled by creating dummy files on the target device:
- Create '/tmp/flashize-env-debug' to trace the user-supplied script.
- Create '/tmp/flashize-ext-debug' to trace environment setup.
- Create '/tmp/flashize-debug' to trace file extraction.

