# P1P2 Finder

A lightweight Windows utility that discovers HPSDR **Protocol 1** and **Protocol 2** radios on your local network. Useful when you don't know which IP address your radio has picked up, or when you want to verify a radio is reachable before firing up Thetis, piHPSDR, SparkSDR, or any other SDR client.

Written by **Brent Crier (N9BC)**.

[![Donate via PayPal](https://img.shields.io/badge/Donate-PayPal-0070BA?logo=paypal&logoColor=white)](https://paypal.me/n9bc)

If this tool saves you time, a small tip is always appreciated — **[paypal.me/n9bc](https://paypal.me/n9bc)** 73!

## Features

- Scans every active IPv4 network interface in parallel — no need to pick the right NIC by hand.
- Sends both Protocol 1 (Metis) and Protocol 2 discovery packets in a single sweep.
- **Passive Listen** mode — binds the discovery port and decodes replies that are already flying around on the wire. Great for watching a radio without interrupting an active Thetis session.
- Manual **IP:Port probe** for radios that live on a subnet different from your PC.
- Live log pane showing packets sent and replies received.
- Decodes MAC address, board type, firmware version, and active/idle status from the reply.

## Requirements

- Windows 10 or Windows 11
- .NET 9 Desktop Runtime (only if running the framework-dependent build; the single-file publish bundles the runtime)

## Download

Pre-built binaries are attached to each release on the [Releases page](../../releases).

## Usage

1. Launch `P1P2Finder.exe`.
2. The left pane lists every active network interface. All are selected by default.
3. Click **Scan** to send a broadcast on each selected interface. Discovered radios appear in the grid.
4. Click **Passive Listen** to just listen on UDP port 1024 without broadcasting — useful when a radio is already in use by another application.
5. To probe a specific address (for example, a radio on a different subnet), type the IP into the **Probe IP** box and click **Probe**.

### Default port

HPSDR discovery uses UDP port **1024**. Change the **Port** field only if you know your radio is listening somewhere else.

### Windows Firewall

On first run, Windows will prompt you to allow the app through the firewall. Accept the prompt for both Private and Public networks if your radio is on a network Windows has classified as Public.

## Notes / Known Quirks

- Radios running original Apache Labs firmware (100D, 7000, 8000) may log SEQ errors if you run an active **Scan** while Thetis is already connected. Use **Passive Listen** mode in that situation.
- HermesLite 2 will not respond to discovery while another host is actively streaming to it.
- ANAN-G2 / Saturn radios respond to discovery even while Thetis is connected.

## License

This software is **closed source** and distributed in binary form only. See [LICENSE](LICENSE) for the full terms.

Reverse engineering, redistribution, and derivative works are not permitted.

## Acknowledgements

- The HPSDR community for documenting the discovery protocols.
- Richard Samphire (MW0LGE / Blitter8 Ltd.) — the original *Discover P1P2 Radios* tool was the inspiration for building an independent implementation.
