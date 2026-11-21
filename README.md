# hermes-slim/wheels

Prebuilt Python wheels that [hermes-slim/hermes](https://github.com/hermes-slim/hermes)
bundles need but PyPI does not ship for one of our targets.

| Package | Version | Target | Why |
|---|---|---|---|
| cryptography | 50.0.2 | macOS x86_64, cp314 | upstream ships arm64-only macOS wheels; built with a static OpenSSL 3.5 LTS, `MACOSX_DEPLOYMENT_TARGET=11.0` |
| cryptography | 50.0.2 | Windows ARM64, cp314 | no win_arm64 wheel upstream; static OpenSSL from vcpkg (`arm64-windows-static-md`) |
| httptools | 0.8.0 | Windows ARM64, cp314 | no win_arm64 wheel upstream |
| firecrawl-anydoc | 0.2.4 | Windows ARM64, abi3 | no win_arm64 wheel upstream (maturin/Rust) |

Wheels are published to the rolling [`latest`](https://github.com/hermes-slim/wheels/releases/tag/latest)
release by `.github/workflows/build.yml`. Bundle builds download that release and pass it to
`uv pip install --find-links`.

To add a package: add a job to `build.yml` that builds, verifies (no non-system shared
libraries, imports cleanly) and uploads the wheel, then add a row here.
