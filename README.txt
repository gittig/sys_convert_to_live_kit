# Convert your current linux environment into a live kit.
#
#
# tools
#   initramfs       cpio.gz
#   root            squashfs + luks + tmpfs + aufs
#   bootloader      syslinux
#
#
# notes
#   This tool has been tested on the following platforms.
#       Debian 10 X86-64
#   Your linux kernel must support aufs and squashfs.
#   Your machine will not automaically boot into the live OS.
#   Your machine will stuck in the initramfs phase during boot.
#   You will be prompted with a busybox shell "/bin/sh", and could manually mount the squashfs root image to "/m1/layer0_squashfs".
#
#
# procedures of building a live kit
#   1. ./00_prepare
#   2. ./0a_build_all
#   3. cd /tmp/0a_build_all.d/ && ./0y_build_boot_iso
#
#
# bugs
#   intended bugs
#       The generated live kit is targeted for a storageless computer with NAS companion.
#       It has no persistent storage.
#       Also, it does not need a mechanism to gracefully umount everything during shutdown.
#   unintended bugs
#       You should run this code in a "normal" linux instance. Running in a live kit linux would not work.
#       This code is likely to fail on non-X86-64 non-Debian linux due to hard-coded paths in "02_build_initramfs".
#       wrong permissions
#           drwxrwxrwt /
#           drwxrwxrwt /initramfs
#
#
# dir_hierarchy
#   root_of_the_boot_driver/
#       boot/                               # for BIOS boot
#           syslinux/
#               isolinux.bin
#               ldlinux.c32
#               syslinux.cfg
#       efi/                                # for UEFI boot
#           boot/
#               bootx64.efi
#               ldlinux.e64
#               syslinux.cfg
#       payload_0/
#           vmlinuz
#           initramfs.cpio.gz
#           root_hc.squashfs.luks           # optional
#           root_lc.squashfs.luks           # optional
#           root.squashfs.luks              # optional
#
#
# references
#   mfslinux
#       tools: cpio.gz, syslinux
#       https://github.com/mmatuska/mfslinux
#       https://downloads.openwrt.org/releases/19.07.1/targets/x86/64/openwrt-19.07.1-x86-64-generic-rootfs.tar.gz
#       https://downloads.openwrt.org/releases/19.07.1/targets/x86/64/openwrt-19.07.1-x86-64-vmlinuz
#
#   linux-live, slax linux
#       tools: cpio.gz, squashfs, aufs, syslinux
#       https://github.com/Tomas-M/linux-live
#       https://github.com/Tomas-M/linux-live/archive/v2.3.tar.gz

