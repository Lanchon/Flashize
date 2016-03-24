## Flashize
### Turn Shell Scripts Into Flashable Android Recovery Zips

#### Features

- Automatically convert shell scripts to flashable zips with a single command.
- Don't mess with `ui_print` crap: standard output and error streams will work just fine.
- Can temporarily override the unpredictable runtime environment offered by the recovery
<br>(shell and userland tools) with a standardized environment bundled within the zipfile.
- Includes pre-built standardized environments for arm, arm64 and x86_64 architectures
<br>based on TWRP 2.7.8 and TWRP 3.0.0 builds.
- Can automatically extract resources from the zipfile before invoking the script.
- Can automatically create a logfile of the output of the script.
- Displays (and possibly logs) the script exit code and reports it back to recovery.
- The script receives the path of the zipfile being flashed as its first parameter.
<br>(Other parameters reserved for future use.)
- Supports various debugging modes for runtime script tracing.
- The conversion tools require Bash shell; they are developed and tested under Linux.
- Flashize is free software published under GPL and LGPL version 3 and later licenses.

<br>

#### Usage: FLASHIZE

Flashize (2016-03-23)

Converts a shell script to a flashable Android recovery zip.

`flashize <input-script> [<output-zip> [<runtime-logfile>]]`

Reads the script from standard input if `<input-script>` is a dash (-).

Names the output zipfile based on `<input-script>` if `<output-zip>` is null or a dash.

Can create a logfile on the device at runtime, according to the value of `<runtime-logfile>`:
- The absolute path of the logfile to be created.
- A relative path or filename to be interpreted against the path of the zipfile being run.
- A dot (.) to use the pathname of the zipfile being run with a '.log' extension.
- Null or a dash to disable logging.

Script debugging modes are enabled by creating dummy files on the target device:
- Create '/tmp/flashize-debug' to trace the user-supplied script.

<br>

#### Usage: FLASHIZE-EXT

Flashize-Ext (2016-03-23)

Converts a shell script to a flashable Android recovery zip. The resulting flashable zip
can automatically extract resources bundled within the zipfile before invoking the script.

`flashize-ext <input-script> <input-zip> <output-zip> <runtime-logfile> <src-dir> <dest-dir> [<extra-src-spec>...]`

Reads the script from standard input if `<input-script>` is a dash (-).

Names the output zipfile based on `<input-script>` if `<output-zip>` is null or a dash.

Can create a logfile on the device at runtime, according to the value of `<runtime-logfile>`:
- The absolute path of the logfile to be created.
- A relative path or filename to be interpreted against the path of the zipfile being run.
- A dot (.) to use the pathname of the zipfile being run with a '.log' extension.
- Null or a dash to disable logging.

Extracts files from the zip at runtime, according to the value of `<src-dir>`:
- Null or a dash: changes to `<dest-dir>` and extracts files matching `<extra-src-spec>` there.
- A path within the zip: changes to `<dest-dir>`/`<src-dir>`, wipes its contents and extracts
  `<src-dir>` there. Also extracts files matching `<extra-src-spec>` to `<dest-dir>`.

Script debugging modes are enabled by creating dummy files on the target device:
- Create '/tmp/flashize-ext-debug' to trace the user-supplied script.
- Create '/tmp/flashize-debug' to trace resource extraction.

<br>

#### Usage: FLASHIZE-ENV

Flashize-Env (2016-03-23)

Converts a shell script to a flashable Android recovery zip. The resulting flashable zip
can temporarily override the unpredictable runtime environment offered by the recovery
(shell and userland tools) with a standardized environment bundled within the zipfile.

`flashize-env <input-script> <env-spec> [<output-zip> [<runtime-logfile>]]`

Reads the script from standard input if `<input-script>` is a dash (-).

Can bundle a runtime environment (shell and userland tools) and temporarily override the
environment offered by the recovery at runtime, according to the value of `<env-spec>`:
- The name (without extension) of an environment provided in Flashize's 'env' directory.
- The path of a user-provided zipfile containing the runtime environment.
- Null or a dash to disable overriding of the environment.

Names the output zipfile based on `<input-script>` if `<output-zip>` is null or a dash.

Can create a logfile on the device at runtime, according to the value of `<runtime-logfile>`:
- The absolute path of the logfile to be created.
- A relative path or filename to be interpreted against the path of the zipfile being run.
- A dot (.) to use the pathname of the zipfile being run with a '.log' extension.
- Null or a dash to disable logging.

Script debugging modes are enabled by creating dummy files on the target device:
- Create '/tmp/flashize-env-debug' to trace the user-supplied script.
- Create '/tmp/flashize-ext-debug' to trace environment setup.
- Create '/tmp/flashize-debug' to trace resource extraction.

