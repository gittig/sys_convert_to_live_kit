# Convert your current linux environment into a live kit.
#
#
# tools
#   initramfs       cpio.gz
#   root            squashfs + tmpfs + aufs
#   bootloader      syslinux
#
#
# notes
#   I'll probably rarely update this public repository.
#   But I am using this code to build RAM-only computers as my daily driver.
#   It is done.
#
#   This tool has been tested on the following platforms.
#       Debian 10 X86-64
#
#   Your linux kernel must support aufs and squashfs.
#   Your machine will not automaically boot into the live OS.
#   Your machine will stuck in the initramfs phase during boot.
#   You will be prompted with a busybox shell "/bin/sh", and need to manually mount the squashfs root image to "/m1/layer0_squashfs".
#
#
# procedures of building a live kit
#   1. build a statically linked busybox, and copy it as "/tmp/busybox".
#   2. locate "ldlinux.e64" from syslinux distro, and copy it as "/tmp/ldlinux.e64". It seems missing from the Debian package repo.
#   3. locate "syslinux.efi" from syslinux distro, and copy it as "/tmp/syslinux.efi". It seems missing from the Debian package repo.
#   4. ./01_prepare
#   5. ./02_build_initramfs
#   6. ./03_build_root
#   7. ./04_build_package
#   8. cd /tmp/04_build_package_safdsdfcdsweacSAFDWE/ && ./05b_build_boot_iso
#
#
# bugs
#   intended bugs
#       The generated live kit is targeted for a storageless computer with NAS companion.
#       There is no persistent storage.
#       Also, it does not need a proper shutdown mechanism to gracefully umount everything.
#   unintended bugs
#       You should run this code in a "normal" linux instance. Running in a live kit linux would not work.
#       This code is likely to fail on non-X86-64 non-Debian derived linux distros due to hard-coded paths in "02_build_initramfs".
#
#
# dir_hierarchy
#   root_of_the_boot_driver/
#       boot/               # for BIOS boot
#           syslinux/
#               ...
#       efi                 # for UEFI boot
#           boot/
#               ...
#       payload_0/
#           vmlinuz
#           root.squashfs (optional)
#           initramfs.cpio.gz
#               init
#
#
# authors
#   forked from linux-live https://github.com/Tomas-M/linux-live
#   written by "gittig"    https://github.com/gittig/
#
#
# references
#   mfslinux
#       tools: cpio.gz, syslinux
#       https://github.com/mmatuska/mfslinux
#       https://downloads.openwrt.org/releases/19.07.1/targets/x86/64/openwrt-19.07.1-x86-64-generic-rootfs.tar.gz
#       https://downloads.openwrt.org/releases/19.07.1/targets/x86/64/openwrt-19.07.1-x86-64-vmlinuz
#
#   linux-live
#       tools: cpio.gz, squashfs, aufs, syslinux
#       https://github.com/Tomas-M/linux-live
#       https://github.com/Tomas-M/linux-live/archive/v2.3.tar.gz

