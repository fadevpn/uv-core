# Ultraviolet


## License

[Mozilla Public License Version 2.0](https://github.com/fadevpn/uv-core/blob/main/LICENSE)

## Documentation

WIP; [xray-core docs](https://xtls.github.io)

## Getting started

WIP

## GUI Clients

- Ultraviolet
  - iOS, macOS, Android: [Ultraviolet](https://github.com/fadevpn/ultraviolet)
  - Windows, Linux: [Ultraviolet](https://github.com/fadevpn/ultraviolet-desktop)
 
Any other client is also compatible as long as it has either VLESS or Hysteria2: 
[Check XTLS for a more extensive list of clients](https://github.com/XTLS/Xray-core#gui-clients)

## Contributing

Unless directly related to ultraviolet, contribute to the upstream - [Xray-core](https://github.com/XTLS/Xray-core/blob/main/CODE_OF_CONDUCT.md)

## Credits

[UV-core](#) (you are here) -> which is a fork of [Xray-core](https://github.com/XTLS/Xray-core/releases/tag/v1.0.0) -> which is a fork of [v2fly-core 9a03cc5](https://github.com/v2fly/v2ray-core/commit/9a03cc5c98d04cc28320fcee26dbc236b3291256)...

For third-party projects used in [UV-core](https://github.com/fadevpn/uv-core), check your local or [the latest go.mod](https://github.com/fadevpn/uv-core/blob/main/go.mod).

### Bundled Third-Party Components Redistribution

**Certain optional features dynamically load third-party components. These optional components are separate works distributed under their own licenses, and are bundled into the ZIP package for ease of use. Users may replace these components under the licenses from these components.**

These components include:

#### Wintun

This distribution contains unmodified official precompiled and pre-signed Wintun binaries.

- Project: Wintun
- Copyright: Copyright (C) 2018-2021 WireGuard LLC. All Rights Reserved.
- Redistribution License: Prebuilt Binaries License (PBL) bundled with official precompiled and pre-signed binaries from wintun.net
- Component(s): wintun.dll
- Source: https://www.wintun.net/
- Included in:
  - Windows x86 (windows-32, win7-32)
  - Windows x86-64 (windows-64, win7-64)
  - Windows AArch64 (windows-arm64)
- Notes: Wintun is an optional runtime-loaded component only used for TUN inbound functionality on supported Windows platforms.

## One-line Compilation

### Windows (PowerShell)

```powershell
$env:CGO_ENABLED=0
go build -o xray.exe -trimpath -buildvcs=false -ldflags="-s -w -buildid=" -v ./main
```

### Linux / macOS

```bash
CGO_ENABLED=0 go build -o xray -trimpath -buildvcs=false -ldflags="-s -w -buildid=" -v ./main
```

### Docker (Linux amd64)

```bash
docker compose build
```

or:

```bash
docker build -t pkg.dev/uviolet/core:custom ./core
docker build -t pkg.dev/uviolet/supervisor:custom ./supervisor
```

### Reproducible Releases

Make sure that you are using the same Go version, and remember to set the git commit id (7 bytes):

```bash
CGO_ENABLED=0 go build -o xray -trimpath -buildvcs=false -gcflags="all=-l=4" -ldflags="-X github.com/xtls/xray-core/core.build=REPLACE -s -w -buildid=" -v ./main
```

For Android:

```bash
GOOS=android GOARCH=arm64 CGO_ENABLED=1 CC=/path/to/aarch64-linux-android24-clang go build -o xray -trimpath -buildvcs=false -gcflags="all=-l=4" -ldflags="-X github.com/xtls/xray-core/core.build=REPLACE -s -w -buildid= -checklinkname=0" -v ./main
GOOS=android GOARCH=amd64 CGO_ENABLED=1 CC=/path/to/x86_64-linux-android24-clang go build -o xray -trimpath -buildvcs=false -gcflags="all=-l=4" -ldflags="-X github.com/xtls/xray-core/core.build=REPLACE -s -w -buildid= -checklinkname=0" -v ./main
```

If you are compiling a 32-bit MIPS/MIPSLE target, use this command instead:

```bash
CGO_ENABLED=0 go build -o xray -trimpath -buildvcs=false -gcflags="-l=4" -ldflags="-X github.com/xtls/xray-core/core.build=REPLACE -s -w -buildid=" -v ./main
```
