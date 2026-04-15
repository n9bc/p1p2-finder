# P1P2 Finder

A lightweight Windows utility that discovers HPSDR **Protocol 1** and **Protocol 2** radios on your local network. Useful when you don't know which IP address your radio has picked up, or when you want to verify a radio is reachable before firing up Thetis, piHPSDR, SparkSDR, or any other SDR client.

Written by **Brent Crier (N9BC)**.

[![Donate via PayPal](https://img.shields.io/badge/Donate-PayPal-0070BA?logo=paypal&logoColor=white)](https://paypal.me/n9bc)

If this tool saves you time, a small tip is always appreciated — **[paypal.me/n9bc](https://paypal.me/n9bc)** 73!

## Features

- Scans every active IPv4 network interface in parallel — no need to pick the right NIC by hand.
- Sends both Protocol 1 (Metis) and Protocol 2 discovery packets in a single sweep.
- Manual **Check** of a specific IP address for radios that live on a subnet different from your PC.
- **Program IP** (Protocol 1 radios) — change a radio's static IP address right-click on a discovered radio in the grid.
- Live log pane with right-click **Copy / Copy All / Clear**.
- Decodes MAC address, board type, firmware version, and active/idle status from the reply.
- **Help** menu with direct links to donate and to the GitHub page, plus an About dialog showing the installed version.

## Requirements

- Windows 10 or Windows 11
- .NET 9 Desktop Runtime (only if running the framework-dependent build; the self-contained single-file publish bundles the runtime)

## Download

Pre-built binaries are attached to each release on the [Releases page](../../releases). Pick the small framework-dependent zip if you already have (or are willing to install) the .NET 9 Desktop Runtime; otherwise grab the self-contained build.

## Usage

1. Launch `P1P2Finder.exe`.
2. The left pane lists every active network interface. All are selected by default.
3. Click **Probe** to send a broadcast on each selected interface. Discovered radios appear in the grid.
4. To check a specific address (for example, a radio on a different subnet), type the IP into the **Check IP** box and click **Check**.
5. Right-click a discovered radio and choose **Program IP...** to change its static IP address. *Protocol 1 radios only.* Close any connected SDR application first — the radio will reboot on its new address.

### Default port

HPSDR discovery uses UDP port **1024**. Change the **Port** field only if you know your radio is listening somewhere else.

### Windows Firewall

On first run, Windows will prompt you to allow the app through the firewall. Accept the prompt for both Private and Public networks if your radio is on a network Windows has classified as Public.

## Notes / Known Quirks

- A radio that is actively connected to an SDR application (Thetis, SparkSDR, etc.) will typically not respond to discovery. Close the SDR app, then run **Probe**.
- HermesLite 2 will not respond to discovery while another host is actively streaming to it.
- ANAN-G2 / Saturn radios generally respond to discovery even while Thetis is connected.
- **Program IP** is experimental — verify behavior on a single radio before relying on it. Setting an invalid IP (e.g., `0.0.0.0`) will leave the radio unreachable until it is reset via its hardware reset jumper/button.

## License

This software is **closed source** and distributed in binary form only. See [LICENSE](LICENSE) for the full terms.

Reverse engineering, redistribution, and derivative works are not permitted.

## Acknowledgements

- The HPSDR community for documenting the discovery protocols.
- Richard Samphire (MW0LGE / Blitter8 Ltd.) — the original *Discover P1P2 Radios* tool was the inspiration for building an independent implementation.
