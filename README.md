# Docker configuration for FME Desktop

Provides `Dockerfile`s and `docker-compose.yml` files to
automatically install specified versions of Safe Software's
**FME Desktop** product into corresponding **Docker** containers
on a Linux or other UNIX-like host running an X server.  When
started, these containers will run *FME Workbench*, from which the
**FME Data Inspector** and subordinate *FME Workbench* processes
may be subsequently launched.

This configuration mounts your home directory on your host by
default, so you'll have full access to any workspaces or data
therein.  You can change this in the `docker-compose.yml` file if
you wish.

This solution will probably work for macOS with an appropriate
environment configuration.  At minimum, you will need to install
**XQuartz**, and set/export your `DISPLAY` environment variable.
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
5. Launch *FME Workbench*: `docker-compose up`
6. License your installation in the usual manner.
7. Enjoy!