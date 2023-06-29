# Packer ubuntu 22.04.2

This repo aims to provide an example of a packer build for `ubuntu-20.04.2`.

## Requirements

- [rtx](https://github.com/jdxcode/rtx)
- [virtualbox](https://www.virtualbox.org/) (6)
- [vagrant](https://www.virtualbox.org/) (2.3.7)

```sh
$ rtx install
```

Optionnaly you can install:

- [virtualbox-guest-additions-iso](https://www.virtualbox.org/manual/ch04.html)

## Getting started

First you must build packer image:

```sh
$ ./scripts/build-packer-image.sh
virtualbox-iso.ubuntu_22_04_2: output will be in this color.

==> virtualbox-iso.ubuntu_22_04_2: Retrieving Guest additions
==> virtualbox-iso.ubuntu_22_04_2: Trying /usr/share/virtualbox/VBoxGuestAdditions.iso
==> virtualbox-iso.ubuntu_22_04_2: Trying /usr/share/virtualbox/VBoxGuestAdditions.iso
==> virtualbox-iso.ubuntu_22_04_2: /usr/share/virtualbox/VBoxGuestAdditions.iso => /usr/share/virtualbox/VBoxGuestAdditions.iso
==> virtualbox-iso.ubuntu_22_04_2: Retrieving ISO
==> virtualbox-iso.ubuntu_22_04_2: Trying http://releases.ubuntu.com/22.04.2/ubuntu-22.04.2-live-server-amd64.iso
==> virtualbox-iso.ubuntu_22_04_2: Trying http://releases.ubuntu.com/22.04.2/ubuntu-22.04.2-live-server-amd64.iso?checksum=sha256%3A5e38b55d57d94ff029719342357325ed3bda38fa80054f9330dc789cd2d43931
...
```

Then you can import and launch image to vagrant to test it:

```sh
$ ./scripts/import-vagrant-box.sh
==> box: Box file was not detected as metadata. Adding it directly...
==> box: Adding box 'packer-build-baremetal-ubuntu-22.04.2-amd64' (v0) for provider:
    box: Unpacking necessary files from: file:///home/alexandre.marre/Documents/packer-ubuntu-22-04/output-vagrant/package.box
==> box: Successfully added box 'packer-build-baremetal-ubuntu-22.04.2-amd64' (v0) for 'virtualbox'!
$ vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'packer-build-baremetal-ubuntu-22.04.2-amd64'...
==> default: Matching MAC address for NAT networking...
==> default: Setting the name of the VM: packer-ubuntu-22-04_default_1688047362301_39369
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: ubuntu
    default: SSH auth method: password
    default:
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
    default: The guest additions on this VM do not match the installed version of
    default: VirtualBox! In most cases this is fine, but in rare cases it can
    default: prevent things such as shared folders from working properly. If you see
    default: shared folder errors, please make sure the guest additions within the
    default: virtual machine match the version of VirtualBox you have installed on
    default: your host and reload your VM.
    default:
    default: Guest Additions Version: 6.0.0 r127566
    default: VirtualBox Version: 6.1
==> default: Mounting shared folders...
    default: /vagrant => /home/alexandre.marre/Documents/packer-ubuntu-22-04
```

Finally you can connect to the VM with `password=password` and try the image created:

```sh
vagrant ssh
Welcome to Ubuntu 22.04.2 LTS (GNU/Linux 5.15.0-76-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Thu Jun 29 14:02:57 UTC 2023

  System load:  0.640625           Processes:             119
  Usage of /:   26.8% of 18.07GB   Users logged in:       0
  Memory usage: 18%                IPv4 address for eth0: 10.0.2.15
  Swap usage:   0%

  => There is 1 zombie process.


Expanded Security Maintenance for Applications is not enabled.

56 updates can be applied immediately.
To see these additional updates run: apt list --upgradable

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


ubuntu@ubuntu:~$
```

## Destroy vagrant VM

If you want to stop vagrant VM you must execute:

```sh
$ vagrant destroy -f
```

## Inspirations

- [vagrant-ubuntu/packer/ubuntu-22.04-virtualbox](https://github.com/alvistack/vagrant-ubuntu/blob/10eba983edf82df1a43ae7a74ad309ed39fde3f0/packer/ubuntu-22.04-virtualbox/)

## Licence

[MIT](./LICENSE)