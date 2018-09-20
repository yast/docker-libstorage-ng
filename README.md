# The libstorage-ng Testing Image

[![Build Status](https://travis-ci.org/yast/docker-libstorage-ng.svg?branch=master)](https://travis-ci.org/yast/docker-libstorage-ng)

This repository builds a [Docker](https://www.docker.com/) image which is used
for running the CI tests at [Travis](https://travis-ci.org/).
The built image is available at the [yastdevel/libstorage-ng](
https://hub.docker.com/r/yastdevel/libstorage-ng/) Docker repository.

## Docker Tags

This repository builds several versions of the image which are published
by the Docker Hub with a different tag.

The images are defined in the `Dockerfile.<tag>` files and published as
`yastdevel/libstorage-ng:<tag>` at the Docker Hub. See the complete [list of tags](
https://hub.docker.com/r/yastdevel/libstorage-ng/tags/) at the Docker Hub.

#### Adding New Versions

When adding a new version of the image:

- Create the respective `Dockerfile.<tag>` file
- Update the `.travis.yml` file so the image is built also at Travis
- Update the [Docker Hub build setting](
  https://hub.docker.com/r/yastdevel/libstorage-ng/~/settings/automated-builds/) to
  build and publish the new image

## Automatic Rebuilds

- The images are rebuilt whenever a commit it pushed to the `master` branch.
  This is implemented via GitHub webhooks.

- Additionally the images are periodically rebuilt to ensure the latest YaST
  packages from the respective  OBS project are used even when the image
  configuration has not been changed.
  The build is triggered by the [docker-trigger-yastdevel-libstorage-ng](
  https://ci.opensuse.org/view/Yast/job/docker-trigger-yastdevel-libstorage-ng/)
  Jenkins job.


## Triggering a Rebuild Manually

If for some reason the automatic rebuilds do not work or you need to fix
a broken build you can trigger rebuild manually.

- Go to the [Build Settings](
https://hub.docker.com/r/yastdevel/libstorage-ng/~/settings/automated-builds/) tab
and press the *Trigger* button next to the *master* branch configuration line.

- If you need to trigger the build from a script check the *Build Triggers*
section at the bottom, press the *Show examples* link to display the `curl`
commands. (The commands contain a secret access token, keep it in a safe place,
do not put it in a publicly visible place.)

## The Image Content

This image is based on the latest openSUSE Tumbleweed image, additionally
it contains the packages needed for running tests for YaST packages written
in Ruby.

## Using the image

The workflow is:

- Copy the sources into the `/usr/src/app` directory.
- Run the `.travis.sh` script.
