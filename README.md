# apt

## About

This repository holds workflows and configurations for building OwnTone Debian
packages and for updating the [Raspberry Pi repository](https://forums.raspberrypi.com/viewtopic.php?t=49928).

Leveraging the magic of Github Actions the workflows can:

- Create pbuilder images for various distributions and architechtures, and use
  these to build OwnTone Debian packages by getting the source, using the Debian
  config in owntone-server/debian and then invoking pdebuild to cross-compile.

- Update the repository with the new packages using reprepro.

## Howto make a new version

1. Edit VER and COMMIT in `pkginfo`.
2. Trigger the `create_dpkg.yml` workflow, and select the targets you want to
   build for. When the workflow is complete, check that it has produced
   artifacts with the expected .deb files.
3. Trigger `update_repo_rpi.yml`. This will load repository data from the latest
   release (revision), update with packages from the latest `create_dpkg.yml`,
   and create a new Github release of the repository with assets for publishing.
   The packages will have been signed using the `RPI_REPO_SECKEY` GitHub secret.

## Howto add a distribution or architechture

1. Add new distro/arch to `create_dpkg.yml`
2. Add new distro/arch to `update_repo_rpi.yml`
3. Edit `repo/rpi/conf/distributions` and `repo/rpi/conf/incoming`.
4. Commit and push changes.

## Credit

This was made with the help of these great guides/resources:

- https://grid.in.th/2020/10/cross-compile-raspbian-x64
- https://jod.al/2015/03/08/building-arm-debs-with-pbuilder/
- https://github.com/mopidy/apt
