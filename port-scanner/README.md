# PortScanner

This project is a threaded TCP port scanner developed in Python to perform network reconnaissance by discovering open ports and their typical services. It highlights core cybersecurity and programming concepts, including socket communication, parallel processing, input sanitization, and efficient CLI interaction.

## Features

- **Fast** — scans ports in parallel (up to 100 at a time) rather than one after another
- **Service names** — open ports are labelled, e.g. `Port 22 (ssh) OPEN`
- **Two modes** — interactive prompts, or a one-line command for scripting
- **Timed** — reports how long each scan took
- **Logged** — every scan is appended to `scan_log.txt` with timestamps
- **Clean exits** — Ctrl+C stops the scan and still reports partial results, no error traceback
- **Input validation** — rejects bad IPs, hostnames that won't resolve, and out-of-range ports

## Requirements

- Python 3.10 or newer (uses `int | None` type hints)
- No third-party libraries — standard library only

## Usage

### Interactive mode

```bash
python scanner.py
```

It will prompt you for a target and a port range, then scan.

### Command-line mode

```bash
python scanner.py 10.0.1.1 -p 1-1024
python scanner.py scanme.nmap.org --ports 20-443 --timeout 0.5
```

| Argument | Description | Default |
|----------|-------------|---------|
| `target` | IP address or hostname to scan | — |
| `-p`, `--ports` | Port range as `START-END` | `1-1024` |
| `-t`, `--timeout` | Per-port timeout in seconds | `0.5` |

If no target is given on the command line, it drops into interactive mode.

## Example output

```
Target resolved to IP: 127.0.0.1

Starting scan on 127.0.0.1 from port 20 to 90 (71 ports, 0.3s timeout)...
Port 22 (ssh) OPEN
Port 80 (http) OPEN

Scan complete.
Total ports scanned: 71
Open ports found:    2
Open ports: 22, 80
Time taken:          0.06 seconds
```

## Logging

Results are appended to `scan_log.txt` in the working directory. Each scan records its start, any open ports found, and a summary line with the elapsed time.

## Notes and limitations

- **IPv4 only.** The tool resolves targets to IPv4 addresses by design; IPv6 is out of scope.
- **Timeout is a trade-off.** A shorter timeout scans faster but may miss slow-responding ports on a laggy network. `0.5s` is a reasonable default for a local network.

## Legal and ethical use

Only scan systems you own or have explicit written permission to test. Port scanning machines you don't have authority over may be illegal in your jurisdiction and against most networks' terms of service. Safe practice targets include your own home lab and `scanme.nmap.org`, which is provided by the Nmap project for testing.

## Author

Prachi Chaurasia
