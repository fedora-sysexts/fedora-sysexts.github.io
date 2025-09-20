---
nav_order: 2
---

# Installing and updating sysexts

## Using `systemd-sysupdate`

You can currently install and update those sysexts using `systemd-sysupdate`.
See each sysext individual page for instructions.

## Experimental standalone sysexts-manager

A standalone sysexts manager is being developed to manage, download and update
sysexts with a more user friendly interface. See
[travier/sysexts-manager](https://github.com/travier/sysexts-manager) for the
work in progress. Note that this project is experimental right now.

## Integration with bootc / Bootable Containers

The planned user experience for using those sysexts on Bootable Container
systems is that they are built as container layers, pushed to a registry as
distinct tags, downloaded, managed and updated in sync with the OS by bootc.
See: [bootc#7](https://github.com/containers/bootc/issues/7) and
[README.containers.md](https://github.com/fedora-sysexts/fedora/blob/main/README.containers.md).
This integration is currently still a work in progress.

## Installing directly via Ignition

On Fedora CoreOS, you can also directly download the sysexts images as files
via Ignition. Here is an example Butane config:

```
variant: fcos
version: 1.5.0
storage:
  files:
      # Make sure to name your sysext as <sysext-name>.raw, without the version here
    - path: "/var/lib/extensions/kubernetes-cri-o-1.32.raw"
      contents:
        # Use the full URL with the version to download the sysext
        source: "https://extensions.fcos.fr/extensions/kubernetes-cri-o-1.32/kubernetes-cri-o-1.32-1.32.3-1.fc42-42-x86-64.raw"
systemd:
  units:
    # Enable systemd-sysext.service to merge the sysexts on boot
    - name: systemd-sysext.service
      enabled: true
    # We will use CRI-O
    - name: docker.socket
      enabled: false
      mask: true
```

For more examples, see:
- [travier/fedora-coreos-kubernetes](https://github.com/travier/fedora-coreos-kubernetes):
  A more complete example deploying Kubernetes on Fedora CoreOS using sysexts.
- [systemd system extension (sysext) tutorial](https://github.com/tormath1/sysext-tutorial):
  A hands-on tutorial from the KubeCon EU 2025 London Contribfest session.
