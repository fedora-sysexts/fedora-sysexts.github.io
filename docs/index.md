---
nav_order: 1
---

# systemd system extensions for Fedora image based systems

**NOTE: This project is a work in progress. Make sure to read the [known
limitations section](https://extensions.fcos.fr/known-issues). Use at your own
risk.**

This project makes sysexts available for Fedora image based systems.

**For the sysexts built from Fedora packages only, see
[extensions.fcos.fr/fedora](https://extensions.fcos.fr/fedora).**

**For the sysexts built from community sources, see
[extensions.fcos.fr/community](https://extensions.fcos.fr/community).**

## What are sysexts?

systemd system extensions (sysexts) are filesystem images that bundle content
(binaries, libraries and configuration files) that can be overlayed on demand
on image based systems. The content of the sysexts are "merged" with the base
content of the OS using an overlayfs mount.

In the context of this project, the sysexts are
[EROFS](https://erofs.docs.kernel.org/en/latest/index.html) disk images that
include content to overlay on top of `/usr`.

If you want to know more about sysexts, you can watch the
[Waiter, an OS please, with some sysext sprinkled on top](https://cfp.all-systems-go.io/all-systems-go-2024/talk/HJLF3C/)
([video](https://media.ccc.de/v/all-systems-go-2024-313-waiter-an-os-please-with-some-sysext-sprinkled-on-top))
talk at All systems go! Berlin 2024.

For a more general description of sysexts, see the
[Extension Images](https://uapi-group.org/specifications/specs/extension_image/)
specification from the UAPI group.

## Can sysexts replace package layering or container builds?

Sysexts can only modify the content in `/usr` and they are enabled relatively
"late" during the boot process, thus they come with some limitations. They can
not be used to:
- install another kernel
- install kernel modules
- make changes to the initrd
- make changes to `/etc`
- add udev rules

If you need to do one of those, you should use package layering or do a
container build. Otherwise, sysexts might be a good fit.

## Available sysexts

You can find all the available sysexts in the list on the side of the
[extensions.fcos.fr/fedora](https://extensions.fcos.fr/fedora) and
[extensions.fcos.fr/community](https://extensions.fcos.fr/community) sub pages.

The sysexts are built for the current stable releases of Fedora, for `x86_64`
and `aarch64`, if the software is available for it.

Some images only target a specific variant (CoreOS, Silverblue, Kinoite, etc.).
When this is the case, it is generally explicit from the name
(`wireshark-silverblue`) or noted in the help text on the sysext page.

The sysexts built only for Fedora CoreOS are also only built for the current
Fedora releases used by each Fedora CoreOS streams (*stable*, *testing* and
*next*).

## Compatibiity

See: [extensions.fcos.fr/compatibility](https://extensions.fcos.fr/compatibility).

## Building, contributing and licenses

See the project
[README](https://github.com/fedora-sysexts/fedora-sysexts.github.io).
