This is a handy script that i use. runs)

## Terminal Muscle Memory (no mouse)
**Line editing**
- `Ctrl+A` start of line
- `Ctrl+E` end of line
- `Alt+B` / `Alt+F` jump word back/forward
- `Ctrl+U` delete to start
- `Ctrl+K` delete to end
- `Ctrl+W` delete previous word
- `Ctrl+Y` paste deleted text
- `Ctrl+L` clear screen

**History**
- `↑ / ↓` previous/next command
- `Ctrl+R` reverse-search history (type, Enter runs)

**Control**
- `Ctrl+C` stop command
- `Ctrl+D` exit shell


---
################################-
## Before I get working Routine
################################

systemctl --failed
journalctl -p 3 -xb | grep -v cosmic
df -h
##If all clean → work with confidence.

## Files & Navigation
- `pwd` — where am I
- `ls` — list files (`ls -la` details/hidden)
- `cd <dir>` — change directory (`cd -` back)
- `tree` — folder tree (install: `sudo apt install tree`)
- `mkdir -p <dir>` — make folders (parents too)
- `touch <file>` — create empty file / update timestamp
- `cp <a> <b>` — copy (`cp -r dirA dirB` folders)
- `mv <a> <b>` — move/rename
- `rm <file>` — delete (`rm -i` confirm, `rm -r` folders)
- `ln -s <target> <link>` — symlink
- `cat <file>` — print file
- `less <file>` — view file (best viewer)
  - `/word` search, `n` next, `q` quit
- `head -n 30 <file>` — first lines
- `tail -n 30 <file>` — last lines
- `tail -f <file>` — follow file updates

**Find / Search**
- `grep -R "text" .` — search text recursively
- `find . -name "*.png"` — find by name
- `find . -type f -mtime -2` — files changed in last 2 days
- `rg "text" .` — fast search (install: `sudo apt install ripgrep`)

**Disk**
- `df -hT` — disk free space + filesystem type
- `du -sh * | sort -h` — what’s big in a folder
- `sudo du -xhd1 /var | sort -h | tail` — what’s big in /var

---

## System & Logs
**At-a-glance**
- `uptime` — load + uptime
- `free -h` — RAM/swap
- `top` — live processes
- `ps aux | head` — process list
- `uname -r` — kernel version
- `hostnamectl` — system identity

**Services**
- `systemctl --failed` — failed services
- `systemctl status <service>` — service details
- `systemctl restart <service>` — restart service (admin)

**Logs**
- `journalctl -b` — logs for this boot
- `journalctl -p 3 -b` — errors this boot (priority 3=err)
- `journalctl -f` — follow logs live
- `dmesg -T | tail -n 80` — kernel messages (hardware/driver)

**Storage devices**
- `lsblk -f` — disks + mounts + filesystems
- `blkid` — show UUIDs (admin-ish)
- `mount | column -t` — what’s mounted

---

## Networking
**Basics**
- `ip a` — interfaces + IPs
- `ip r` — routes
- `ping -c 4 1.1.1.1` — internet reachability
- `ping -c 4 google.com` — DNS + internet test

**Ports / connections**
- `ss -tulpn` — listening ports (what’s running)
- `ss -tpn` — active TCP connections

**DNS tools**
- `dig google.com` — DNS lookup (install: `sudo apt install dnsutils`)
- `resolvectl status` — systemd-resolved DNS status (if used)

**Downloads**
- `curl -I https://example.com` — headers only
- `curl -L -o file.zip URL` — download to file
- `wget URL` — simple downloader

**Wi-Fi**
- `nmcli dev status` — device state
- `nmcli dev wifi list` — available networks
- `nmcli con show` — connections saved

---

## Hardware (and GPU)
**Inventory**
- `lspci | less` — PCI devices (GPU/NIC)
- `lsusb` — USB devices
- `inxi -Fxz` — full summary (install: `sudo apt install inxi`)

**Temps**
- `sensors` — temperatures/fans (install: `sudo apt install lm-sensors` then `sudo sensors-detect`)

**Disks**
- `sudo smartctl -a /dev/nvme0n1` — SMART health (install: `sudo apt install smartmontools`)

**NVIDIA**
- `nvidia-smi` — GPU status, driver version
- `modinfo nvidia | head` — driver module info
- `dkms status` — DKMS modules status (useful after updates)

---

## Packages (APT / DPKG)
- `sudo apt update` — refresh package lists
- `sudo apt upgrade` — upgrade installed packages
- `sudo apt install <pkg>` — install package
- `sudo apt remove <pkg>` — remove package
- `sudo apt purge <pkg>` — remove + config
- `sudo apt autoremove` — remove unused deps
- `apt-cache policy <pkg>` — show repo origin (sanity check)
- `dpkg -l | grep <name>` — list installed matching

**What changed**
- `less /var/log/apt/history.log` — apt install/upgrade history
- `grep "status installed" /var/log/dpkg.log | tail -n 50` — recent installs

---

## Git (daily)
**Core flow**
- `git status` — what changed
- `git add .` — stage all changes
- `git commit -m "message"` — commit
- `git push` — push to remote
- `git pull` — pull from remote

**Useful**
- `git log --oneline --graph --decorate --all | head -n 30`
- `git diff` — see unstaged changes
- `git diff --staged` — see staged changes
- `git restore <file>` — undo unstaged changes
- `git restore --staged <file>` — unstage
- `git branch` — list branches

---

## Security / Sanity
**Users & perms**
- `id` — your uid/gids
- `groups` — your groups
- `ls -la` — permissions view
- `chmod` — change permissions
- `chown` — change ownership

**SSH**
- `ssh -v user@host` — debug SSH
- `ssh-keygen -t ed25519` — generate key
- `ssh-add ~/.ssh/id_ed25519` — add key to agent

**Suspicious network check**
- `ss -tulpn` — what’s listening
- `systemctl --type=service --state=running | less` — running services

---

## No-mouse “help” patterns
- Explain a command: `hawk <cmd>`
- List a category: `hawk net` / `hawk hw` / `hawk sys`
- Search everything: `hawk` then type a word (fzf)

---

## Handy installs (quality of life)
- `sudo apt install fzf ripgrep bat tree inxi`
  - `fzf` = fuzzy search
  - `rg` (ripgrep) = fast text search
  - `bat` = nicer cat (line numbers/highlight)
  - `tree` = directory view
  - `inxi` = hardware summary
