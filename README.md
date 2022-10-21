# Docker configuration for FME Desktop

Provides `Dockerfile`s and `docker-compose.yml` files to
automatically install specified versions of Safe Software's
**FME Desktop** product into corresponding **Docker** containers
on a Linux or other UNIX-like host running an X server.  When
started, these containers will run any **FME Desktop** application.

This configuration mounts your home directory on your host by
default, so you'll have full access to any workspaces or data
therein.  You can change this in the `docker-compose.yml` file if
you wish.

This solution will probably work for macOS with an appropriate
environment configuration.  At minimum, you will need to install
**XQuartz** and set/export your `DISPLAY` environment variable.
Feel free to fork this repository if you need to make changes to
support other desktop operating environments.  If you can do so
without compromising the integrity of the Linux-hosted desktop
environment, please make a pull request and I will be happy to
review your suggested improvements for incorporation into the base
repository.

## Installation and Usage
1. Clone this repository somewhere:
`git clone https://github.com/modgeosys/fme-desktop-docker.git`
2. Change to the fme-workbench directory under the **FME Desktop**
version you wish to install.
3. Modify the `docker-compose.yml` file as you see fit.  The
changes you'll most likely want to make are to the `TIME_ZONE_AREA`
and `TIME_ZONE_LOCATION` arguments so they correspond to your
location.
4. Build the container image: `docker-compose build`
5. Launch **FME Workbench**: `WORKING_DIRECTORY=`*your_working_directory*` COMMAND=fmeworkbench docker-compose up`
6. Launch **FME Quick Translator**: `WORKING_DIRECTORY=`*your_working_directory*` COMMAND=fmequicktranslator docker-compose up`
7. Launch **FME Data Inspector**: `WORKING_DIRECTORY=`*your_working_directory*` COMMAND=fmedatainspector docker-compose up`
8. Launch **FME Help**: `WORKING_DIRECTORY=`*your_working_directory*` COMMAND=fmehelpapp docker-compose up`
9. Launch **FME Licensing Assistant**: `WORKING_DIRECTORY=`*your_working_directory*` COMMAND=fmelicensingassistant docker-compose up`
10. Run an **FME** workspace: `WORKING_DIRECTORY=`*your_working_directory*` COMMAND=fme WORKSPACE=`*your_workspace_fmw*` PARAMETERS=`*your_workspace_parameters*` docker-compose up`
11. License your installation in the usual manner.
12. Enjoy!

## Upgrading
1. `cd `*your_fme-desktop-docker_git_repository_path*
2. `git pull`
3. Merge any `Dockerfile` and `docker-compose.yml` changes with your customizations.
4. Change to the fme-workbench directory under the **FME Desktop**
version you wish to install.
5. `docker-compose down -v`
6. Launch **FME Workbench**: `WORKING_DIRECTORY=`*your_working_directory*` COMMAND=fmeworkbench docker-compose up`
7. Launch **FME Quick Translator**: `WORKING_DIRECTORY=`*your_working_directory*` COMMAND=fmequicktranslator docker-compose up`
8. Launch **FME Data Inspector**: `WORKING_DIRECTORY=`*your_working_directory*` COMMAND=fmedatainspector docker-compose up`
9. Launch **FME Help**: `WORKING_DIRECTORY=`*your_working_directory*` COMMAND=fmehelpapp docker-compose up`
10. Launch **FME Licensing Assistant**: `WORKING_DIRECTORY=`*your_working_directory*` COMMAND=fmelicensingassistant docker-compose up`
11. Run an **FME** workspace: `WORKING_DIRECTORY=`*your_working_directory*` COMMAND=fme WORKSPACE=`*your_workspace_fmw*` PARAMETERS=`*your_workspace_parameters*` docker-compose up`
