# zt-bench — Benchmarks and test suite for zt

Benchmark scripts and results for [zt](https://github.com/midasdf/zt), a minimal terminal emulator in Zig.

## Benchmarks

`bench.sh` — compares zt against st, xterm, alacritty, ghostty under Xvfb.

```sh
# Requires: hyperfine, Xvfb, terminals installed
./bench.sh
```

Measures startup time (hyperfine, 30 runs), throughput (4.7MB dense ASCII), and peak RSS. All tests pinned to 1 CPU core. Includes constrained mode (512MB RAM limit) to simulate RPi Zero 2W.

### Latest results (Intel i5-12450H, 1 core, Xvfb)

#### Startup time (30 runs)

| Terminal | Mean | vs zt |
|----------|------|-------|
| **zt** | **30ms** | 1.0x |
| xterm | 41ms | 1.4x |
| st | 57ms | 1.9x |
| alacritty | 110ms | 3.7x |
| ghostty | 908ms | 30x |

#### Throughput: 4.7MB dense ASCII (5 runs)

| Terminal | Time | MB/s | Peak RSS |
|----------|------|------|----------|
| **zt** | **0.008s** | **568** | **5.7 MB** |
| st | 0.162s | 28 | 24 MB |
| xterm | 0.188s | 24 | 14 MB |
| alacritty | 0.256s | 18 | 180 MB |
| ghostty | 0.992s | 4.6 | 307 MB |

## Integration tests

| Script | Purpose |
|--------|---------|
| `test-xvfb.sh` | Full integration test suite under Xvfb |
| `test-xvfb-local.sh` | Local version (no Docker) |
| `test-apps.sh` | Verify terminal apps (vim, nano, less, btop, etc.) |
| `Dockerfile.test` | Docker environment for CI |

## License

MIT
