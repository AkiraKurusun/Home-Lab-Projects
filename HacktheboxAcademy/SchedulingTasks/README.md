\## Automated System Patch Management Using systemd



Implemented a system-level automation workflow using `systemd` timers and services to perform routine package maintenance on a Linux system. The solution replaces manual update processes with a scheduled, repeatable execution model managed by `systemd`.



The service executes a custom Bash script that performs package index updates, system upgrades, and post-update cleanup operations using `apt-get`. The script includes defensive shell settings (`set -euo pipefail`), basic logging functions, and environment validation to ensure compatibility with Debian-based systems.



Scheduling is handled via a `systemd` timer unit, enabling automated execution after boot and at defined intervals. Logs and execution status are available through `journalctl`, improving observability and troubleshooting capability compared to traditional cron-based approaches.



\### Key Components

\- `mytimer.service`: Executes the update script

\- `mytimer.timer`: Defines execution schedule and recurrence

\- `APT-Update.sh`: System maintenance script

\- `systemctl`: Service and timer lifecycle management

\- `journalctl`: Centralized logging and diagnostics



\---



\## Script Automation (Implementation Notes)



\### Description

The purpose of this exercise was to design a shell script and configure Linux systemd to execute it automatically at system boot, validating understanding of service-based automation and scheduling mechanisms.



\### Difficulties Encountered

Several permission-related issues were encountered during implementation:



\- The script required root-level privileges to execute system updates.

\- Initial execution attempts failed due to insufficient permissions when the script was located in a user directory.

\- The script was moved into a system-level path to align with systemd execution expectations.

\- Executable permissions were applied to the script (`chmod +x`), resolving execution blocking issues.

\- Verification through `journalctl` confirmed successful execution and correct service behavior after remediation.



\### Troubleshooting Approach

\- Identified execution failure via systemd status and journal logs

\- Isolated root cause to file permission and execution context

\- Adjusted file permissions and relocated script to appropriate system directory

\- Validated resolution using `journalctl -u <service>`



\---



\### Bash Script (APT Maintenance Automation)

```bash

\#!/usr/bin/env bash



set -euo pipefail



log() { echo "\[\*] $1"; }

err() { echo "\[!] $1" >\&2; }



if ! command -v apt-get >/dev/null 2>\&1; then

&#x20; err "apt-get not found. This script is for Debian/Ubuntu systems."

&#x20; exit 1

fi



log "Updating package index..."

sudo apt-get update -y



log "Upgrading installed packages..."

sudo apt-get upgrade -y



log "Cleaning up..."

sudo apt-get autoremove -y

sudo apt-get autoclean -y



log "Done."

