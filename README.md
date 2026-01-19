# Cloud Images for Proxmox

Automated builds of cloud-init ready qcow2 images optimized for Proxmox VE. Used by [ProxUI](https://github.com/greenlogles/proxui).

## Supported Images

| Image | Distribution |
|-------|--------------|
| ubuntu-noble-amd64.qcow2 | Ubuntu 24.04 LTS |
| ubuntu-jammy-amd64.qcow2 | Ubuntu 22.04 LTS |
| debian-12-bookworm-amd64.qcow2 | Debian 12 |
| debian-13-trixie-amd64.qcow2 | Debian 13 |
| rocky-10-amd64.qcow2 | Rocky Linux 10 (LVM) |
| rocky-9-amd64.qcow2 | Rocky Linux 9 |
| fedora-43-amd64.qcow2 | Fedora 43 |
| fedora-42-amd64.qcow2 | Fedora 42 |
| freebsd-15.0-ufs-amd64.qcow2 | FreeBSD 15.0 (UFS) |

## Compression

All images use qcow2 internal compression (`qemu-img convert -c`), reducing file sizes while maintaining full Proxmox compatibility. No decompression required before import.

## Usage

Download from [Releases](../../releases) and import to Proxmox:

```bash
qm importdisk <vmid> <image>.qcow2 <storage>
```

## Build

Images are automatically built on push to `main` and published as GitHub releases with SHA256 checksums.
