# NIGHTFALL

**Hard · Web / Linux · Ubuntu Server 24.04 LTS**

Nightfall Analytics maintains a portal for internal research reports. A recent deployment has made the service behave in ways its operators did not expect. Your task is to investigate the designated NIGHTFALL virtual machine and retrieve its user and root flags.

## Learning goals

- Map a small web and SSH attack surface.
- Follow clues in exposed deployment artifacts.
- Trace information across a multi-component report workflow.
- Distinguish a web service account from an interactive Linux user.
- Audit a root-run maintenance workflow and its file permissions.

## Rules of engagement

This is a deliberately vulnerable **local training lab**. Test only the NIGHTFALL VM on an isolated VMware Host-Only or Custom VMnet shared with your Kali VM. Do not bridge the target, forward its ports to the Internet, or test any other system. The target is designed to have no default route in its final practice profile.

## Requirements

- VMware Workstation on Windows/Linux or VMware Fusion on macOS.
- Kali Linux or another authorized test VM.
- Ubuntu Server 24.04 LTS installation media for a manual build.
- At least 2 vCPUs, 2 GB RAM, and 12 GB virtual disk for the target.
- A VMware Host-Only/Custom network with DHCP enabled and no NAT/bridging.

## Deploy

Follow [docs/deployment-vmware.md](docs/deployment-vmware.md) and [docs/networking.md](docs/networking.md). VMware and Packer build automation are not included in this release; use the documented manual installation and provisioning flow. The project has not yet been boot-tested in a VMware guest.

The provisioning scripts require temporary build-time Internet access to install Ubuntu packages and pinned Python dependencies. Disconnect the temporary NAT adapter before starting the exercise and verify the isolated profile as described in the networking guide.

## Start and identify the target

Start the target and Kali on the same isolated VMnet. On Kali, inspect the address on that interface and discover the target on that private subnet. Do not scan other interfaces or networks. The target hostname is `nightfall`; its DHCP address can change between resets.

## Reset

From the target console, run `sudo /opt/nightfall/scripts/reset.sh --confirm`. Reset restores the release's initial database and maintenance queue while preserving the current flags, release identifier, and generated analyst credential. It replaces the database and queue state but does not delete VMware files.

## Troubleshooting and feedback

See [docs/troubleshooting.md](docs/troubleshooting.md). Include the release identifier, the exact command or page that failed, and relevant redacted service logs when reporting a reproducible issue. Never include flag values or private host information.

Hints and the solution guide are kept in `docs/`; avoid opening them if you want to solve the lab unaided.
