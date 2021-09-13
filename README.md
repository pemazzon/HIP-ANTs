# app-template

`app-template` is the template repository for integrating new apps into the HIP. It can be used as a template when creating a new repository for an app. The provided Docker file must be completed and modified for the new app that you wish to integrate. The following modifications are needed:

## Dockerfile modifications

All parts of the Dockerfile marked with `<>` must be completed:

1. `<base-image:version>` the following base images are available (all base images are based on Ubuntu 20.04 LTS):
    - `nc-webdav:1.6.0-1`: if you don't need matlab-runtime
    - `matlab-runtime:R2020a_u6`: if you need matlab-runtime version 2020a update 6
    - `matlab-runtime:R2020b_u5`: if you need matlab-runtime version 2020b update 5

2. `<app>`: ubuntu package of the app to be installed. If such a package does not exist, please execute the necessary commands to install it as part of this `RUN` command. Make sure to purge all unnecessary packages at the end to keep the docker image as compact as possible.

3. `<no>`: whether the app must be ran from a terminal. If yes, change to `yes`.

4. `</path/to/app/executable>`: absolute path to the app executable.

5. `<app_process_name>`: the exact name of the app process (if several use the parent process). You can find out by installing the app on Ubuntu 20.04 and running the command `ps faux`. This information is important for the health check as well as synchronizing files to Nextcloud after the `app` exited.

6. `<app_files .app_config>`: list of files and folders necessary for the app to function and retain its state (database, preferences, etc.). These files and folders will be synced to Nextcloud and mounted into the container.
