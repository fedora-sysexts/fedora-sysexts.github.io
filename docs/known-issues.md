---
nav_order: 9
---

# Know issues and common errors

## Use `systemctl restart systemd-sysext.service` to refresh sysexts on Fedora 41

On Fedora 41 based images, make sure to use `systemctl restart
systemd-sysext.service` instead of `systemd-sysext merge`. `systemd-sysext
unmerge` is safe to use.

This issue is fixed in systemd v257 which landed in Fedora 42. See:
- <https://github.com/coreos/fedora-coreos-tracker/issues/1744>
- <https://github.com/systemd/systemd/issues/34387>
- <https://github.com/systemd/systemd/pull/34414>
- <https://github.com/systemd/systemd/pull/35132>

## Current limitation of systemd-sysupdate

While installing and updating via `systemd-sysupdate` works, this also has a
few limitations:
- The sysexts are enabled "statically" for all deplpoyments and if you rebase
  between major Fedora versions, the sysexts will not match the Fedora release
  and will not be loaded until you update again using `systemd-sysupdate`.
- The SELinux policy is currently incomplete for `systemd-importd`, used by
  `systemd-sysupdate`, which thus prevent us from running updates as a service
  in the background for now. See:
  - <https://github.com/fedora-selinux/selinux-policy/pull/2604>
  - <https://github.com/fedora-selinux/selinux-policy/issues/2622>

## Failed to read metadata for image ...: No medium found

If you encounter this error, it likely means that you have set your sysext
image with the full name in the `/var/lib/extensions` directory.
`systemd-sysext` expects the sysexts images to be named only with their own
name, without any version (thus why we use the `/var/lib/extensions.d`
directory in the general case).
