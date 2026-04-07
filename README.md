# zt-bench — Benchmarks and test suite for zt

Benchmark scripts and results for [zt](https://github.com/midasdf/zt), a minimal terminal emulator in Zig.

## Benchmarks

`bench.sh` — compares zt against st, xterm, alacritty, ghostty under Xvfb.

```sh
# Requires: hyperfine, Xvfb, terminals installed
./bench.sh
```

Measures startup time (hyperfine, 30 runs), throughput (4.7MB dense ASCII), and peak RSS. All tests pinned to 1 CPU core. Includes constrained mode (512MB RAM limit) to simulate RPi Zero 2W.

### Latest results (Intel i5-12450H, 1 core, X11 :0)

#### Startup time (30 runs)

| Terminal | Mean | vs zt |
|----------|------|-------|
| **zt** | **5.3ms** | 1.0x |
| xterm | 23ms | 4.2x |
| st | 43ms | 8.1x |
| foot | 46ms | 8.6x |
| alacritty | 123ms | 23x |
| kitty | 206ms | 39x |
| ghostty | 379ms | 71x |

#### Throughput: 4.7MB dense ASCII (5 runs)

| Terminal | Time | MB/s | Peak RSS |
|----------|------|------|----------|
| **zt** | **52ms** | **88** | **5.7 MB** |
| foot | 116ms | 40 | 26 MB |
| st | 160ms | 29 | 25 MB |
| xterm | 180ms | 26 | 13 MB |
| alacritty | 222ms | 21 | 131 MB |
| kitty | 306ms | 15 | 146 MB |
| ghostty | 598ms | 8 | 229 MB |

#### Throughput: 2.9MB TrueColor (5 runs)

| Terminal | Time | MB/s | vs zt |
|----------|------|------|-------|
| **zt** | **53ms** | **55** | 1.0x |
| foot | 107ms | 27 | 2.0x |
| xterm | 129ms | 23 | 2.4x |
| st | 130ms | 22 | 2.4x |
| alacritty | 196ms | 15 | 3.7x |
| kitty | 280ms | 10 | 5.3x |
| ghostty | 534ms | 5 | 10.1x |

#### Throughput: 3.0MB Unicode/CJK (5 runs)

| Terminal | Time | MB/s | vs zt |
|----------|------|------|-------|
| **zt** | **58ms** | **52** | 1.0x |
| foot | 126ms | 24 | 2.2x |
| st | 126ms | 24 | 2.2x |
| xterm | 142ms | 21 | 2.5x |
| alacritty | 200ms | 15 | 3.4x |
| kitty | 292ms | 10 | 5.0x |
| ghostty | 480ms | 6 | 8.3x |

#### Idle memory (PSS)

| Terminal | RSS | PSS | vs zt |
|----------|-----|-----|-------|
| **zt** | **5.0 MB** | **2.3 MB** | 1.0x |
| xterm | 11 MB | 4.3 MB | 1.8x |
| foot | 24 MB | 10 MB | 4.2x |
| st | 25 MB | 13 MB | 5.3x |
| alacritty | 107 MB | 33 MB | 14x |
| kitty | 135 MB | 51 MB | 22x |
| ghostty | 215 MB | 87 MB | 38x |

## Integration tests

| Script | Purpose |
|--------|---------|
| `test-xvfb.sh` | Full integration test suite under Xvfb |
| `test-xvfb-local.sh` | Local version (no Docker) |
| `test-apps.sh` | Verify terminal apps (vim, nano, less, btop, etc.) |
| `Dockerfile.test` | Docker environment for CI |

## License

MIT
