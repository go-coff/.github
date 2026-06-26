<p align="center"><img src="https://raw.githubusercontent.com/go-coff/brand/main/social/go-coff.png" alt="go-coff" width="640"></p>

<h1 align="center">go-coff</h1>
<p align="center">Pure-Go tooling for the <strong>PE/COFF</strong> object &amp; executable format as used by <strong>UEFI</strong> — link, convert, append, pack and sign EFI binaries with <strong>no cgo</strong> and <strong>no binutils / LLD / objcopy / sbsign</strong>.</p>
<p align="center">
  <img src="https://img.shields.io/badge/Go-1.26-00ADD8?style=flat-square&logo=go&logoColor=white">
  <img src="https://img.shields.io/badge/license-BSD--3--Clause-0A6E96?style=flat-square">
  <a href="https://go-coff.github.io/"><img src="https://img.shields.io/badge/site-go--coff.github.io-0079A8?style=flat-square"></a>
  <a href="https://go-coff.github.io/docs/"><img src="https://img.shields.io/badge/docs-mkdocs-0079A8?style=flat-square"></a>
</p>

## What this is

go-coff builds and manipulates **PE32+/EFI** images in pure Go, without a C
toolchain. It is the pure-Go replacement for the `lld-link /subsystem:efi_application`
→ `objcopy --add-section` → `sbsign` pipeline: turn relocatable objects (or a
position-independent ELF) into a self-contained EFI application, assemble Unified
Kernel Images, emit bare-metal images, compress an EFI binary, and Authenticode-sign
for Secure Boot.

## Repositories

| Repo | What it is |
| --- | --- |
| [`peln`](https://github.com/go-coff/peln) | The core **library**: a PE/COFF linker (relocatable `.o` / PIE → PE32+/EFI), a section **appender** (`objcopy --add-section`, for UKI assembly), and `fwimg` for non-UEFI bare-metal images (flat binary, Motorola SREC, Intel HEX, U-Boot uImage). Zero deps, 100% coverage. |
| [`pectl`](https://github.com/go-coff/pectl) | The reference **CLI** over `peln`: link, convert (PIE → PE), `objcopy`, append, pack and Authenticode-**sign** PE32+/EFI binaries — a single static binary, no C toolchain. 100% coverage. |
| [`efipack`](https://github.com/go-coff/efipack) | A self-extracting EFI **compressor** — a UPX-equivalent for the PE32+/EFI format, intended to mitigate the EDK2 OVMF `CpuPageTableLib` `#GP` on `LoadImage`/`StartImage` of large EFI binaries. Host side shipped; runtime decompressor stub in progress. |
| [`stub`](https://github.com/go-coff/stub) | A UEFI **Unified Kernel Image stub** (TinyGo + a thin asm shim) that chain-loads an embedded `.linux` section — removing `systemd-stub` as a build dependency. Boots under OVMF on x86_64 and aarch64. |

Every library is pure Go (`CGO_ENABLED=0`), dependency-light, and **BSD-3-Clause**.
`peln`, `pectl` and `efipack` validate on all six 64-bit Go targets
(amd64 · arm64 · riscv64 · loong64 · ppc64le · s390x); `s390x` makes the
big-endian leg a real endianness test of the little-endian PE/COFF codec.

## Links

- 🌐 Landing — <https://go-coff.github.io/>
- 📖 Docs — <https://go-coff.github.io/docs/>
- 🎨 Brand assets — <https://github.com/go-coff/brand>

---
<p align="center"><sub>Branding in <a href="https://github.com/go-coff/brand">go-coff/brand</a>. BSD-3-Clause.</sub></p>
