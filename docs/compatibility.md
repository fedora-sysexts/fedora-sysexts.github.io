---
nav_order: 8
---

# Compatibility

## Fedora image based variants

The primary target for those sysexts are the official Fedora imaged based
variants (Fedora CoreOS, Fedora Atomic Desktops, Fedora IoT), whether they are
Bootable Container (bootc) systems or classic ostree/rpm-ostree ones.

Those systems are the primary target as it is those images that are used as the
base to figure out the dependencies to include in the sysexts.

## Universal Blue images (Bazzite, Bluefin, Aurora, uCore)

The sysexts should also work with the images from the Universal Blue project
(Bazzite, Bluefin, Aurora, uCore) as they are derived from the Fedora Bootable
Container (bootc) images used to build those sysexts.

## Other images derived from Fedora Bootable Container

The sysexts should also work with images derived from a Fedora Bootable
Container (bootc) image but you will have to verify the compatibility on a per
image basis.

## Other Fedora image mode systems

The sysexts may also work with other Fedora image based systems such as those
built using [mkosi](https://github.com/systemd/mkosi), but you will have to
verify compatibility on a per image basis and potentially rebuilt the sysexts
to include missing dependencies.

## Per-sysext compatibility notes

Make sure to look at the compatibility notes for each sysext. Some are only
meant to be used on specific Fedora image based variants.
