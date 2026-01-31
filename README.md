# Dynamic Nftables

Dynamic Nftables is a small project to make managing nftable rules slightly easier for your desktop or (secure) server.

It uses base rules taken from the Archlinux default `/etc/nftable.conf`.

## Usage

Note that this project by default OVERRIDES your default systemd nftable service and how it fires. If you modify the service yourself make sure that this override is not overriding or messing up your own modifications.

*Note* this project assumes you will have 3 different locations available for writing rules and follows Systemd-like designations for these files. `/etc/nftables/` for user/admin specified nftable rules, `/usr/lib/nftables` for package/distro provided nftable rules, and `/run/nftables/` for generated nftable rules. Each of these directories have an identical directory layout. For the rest of this readme the `<root>` directory will refer to any of the 3.

### Static Rules

- Static rules are constant (always on) rules
- Stored under `<root>/static`.
- Activated when `nftables.service` activates.
- Files are loaded in the order `/usr/lib/nftables/`, `/etc/nftables/`, and finally `/run/nftables/` with overlapping names overwriting a previously occuring entry
- Files are sorted in the same manner as systemd before being written.

### Dynamic Rules

- Dynamic rules are nftable rules loadable as systemd services.
- Stored under `<root>/dynamic`
- Activated via `nft-forward-rule@<file>.service`, `nft-input-rule@<file>.service`, and `nft-output-rule@<file>.service`
- Files are loaded in the order `/usr/lib/nftables/`, `/etc/nftables/`, and finally `/run/nftables/` with overlapping names overwriting a previously occuring entry
- Files MUST be written as if they are inside of a chain (because they will loaded as such)
