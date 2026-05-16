# Resolver Royale

A cross-platform DNS benchmark that races 22 public resolvers against your current DNS and tells you which one is actually fastest from your location.

![Resolver Royale](./assets/banner.png)

## Your DNS Might Be Slower Than It Should Be

ISP-assigned DNS resolvers are often the bottleneck you never think to check. Switching to a faster public resolver can shave milliseconds off every single network request your machine makes — page loads, API calls, `git fetch`, package installs. The catch: "fastest" depends entirely on where you are. Cloudflare wins in some regions, Google in others, Quad9 somewhere else. Without measuring from your own machine, you're guessing.

## Benchmark, Rank, Apply

Resolver Royale fires 50 queries per server (5 iterations across 10 popular domains) against 22 DNS providers — including your current resolver — and scores each one on a weighted composite of average latency, median latency, jitter, and reliability. Results are ranked with letter grades (A+ through F), and the winner comes with a copy-paste command to switch your DNS immediately.

Supported on macOS, Ubuntu/Debian, and RHEL/Rocky/CentOS.

## Example

```
  Current DNS:  192.168.1.1
  Source file:  /etc/resolv.conf

  Benchmarking 23 servers — this takes ~1–2 minutes …

  Rank  Name                      IP               Avg    Med    Jitter  Rel%   Score  Grade
  ────  ────────────────────────  ───────────────  ─────  ─────  ──────  ─────  ─────  ─────
     1  Cloudflare                1.1.1.1          8.2ms  6.0ms  42ms    100%   90.3   A
     2  Google                    8.8.8.8          12.1ms 10.0ms 38ms    100%   87.6   A-
     3  Quad9                     9.9.9.9          15.4ms 12.0ms 51ms    100%   84.1   B+
   ...

  ╔══════════════════════════════════════════════════════════════════╗
  ║  🏆  Fastest DNS: Cloudflare
  ║     IP:          1.1.1.1
  ║     Score:       90.3 (A)
  ╚══════════════════════════════════════════════════════════════════╝
```

## Usage

```bash
# Run the benchmark
./dns-benchmark.sh

# Apply the fastest DNS (requires sudo)
sudo ./dns-benchmark.sh --apply

# Restore DHCP defaults
sudo ./dns-benchmark.sh --restore
```

### Requirements

- `dig` and `bc`

```bash
# Ubuntu/Debian
sudo apt install -y dnsutils bc

# RHEL/Rocky/CentOS
sudo dnf install -y bind-utils bc

# macOS
brew install bind
```

## License

[MIT](LICENSE)

<BR>
