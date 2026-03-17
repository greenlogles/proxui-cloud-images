# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

This repo produces cloud-init ready qcow2 images optimized for Proxmox VE. All images are built via a single GitHub Actions workflow — there is no local build toolchain.

## How It Works

The workflow (`.github/workflows/build-cloud-images.yml`) runs on every push to `main` and:

1. Downloads upstream cloud images from official vendor sources
2. Converts each to compressed qcow2 using `qemu-img convert -c -f qcow2 -O qcow2`
3. Generates SHA256 checksums
4. Publishes a GitHub release tagged `v{YYYYMMDD}-{short-sha}` with all images and checksums

Ubuntu images arrive as `.img` format and are converted. Debian, Rocky, Fedora, and FreeBSD images arrive as `.qcow2` already. FreeBSD additionally requires `unxz` decompression before conversion.

## Adding a New Image

Each image requires three workflow steps: Download, Convert (with `rm` of the `-orig` file), and an entry in the release notes table. The naming convention is `{distro}-{version}-{variant}-amd64.qcow2`. Rocky Linux 10 uses the LVM variant; others use the generic/base cloud variant.

## Local Testing

To test a conversion locally (requires `qemu-utils`):

```bash
qemu-img convert -c -f qcow2 -O qcow2 input-orig.qcow2 output.qcow2
qemu-img info output.qcow2
```

## Proxmox Import

```bash
qm importdisk <vmid> <image>.qcow2 <storage>
```
