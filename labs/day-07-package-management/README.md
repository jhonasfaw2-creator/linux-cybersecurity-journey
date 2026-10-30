# Lab 07 — Linux Package Management with APT and dpkg

## Objective
Practise inspecting installed packages, searching repositories, refreshing package information, simulating software installations, and examining package contents.

## Environment
- Operating system: Ubuntu 26.04.1 LTS (codename: resolute)
- Shell: Zsh
- Package manager: APT 3.2.0 (amd64)
- Low-level package tool: dpkg 1.23.7 (amd64)
- Lab type: Local Linux administration
- Scope: Package inspection and controlled software management

---

## Exercise 1 — Inspect Package Management Tools

**Commands**
```bash
apt --version
dpkg --version
```

**Output**
```
apt 3.2.0 (amd64)
Debian 'dpkg' package management program version 1.23.7 (amd64).
```

**Roles**
- **dpkg** is the low-level tool. It installs, removes, and inspects individual `.deb` files and maintains the package database in `/var/lib/dpkg`. It does not download packages or resolve dependencies.
- **APT** is the high-level tool. It reads repository configuration, downloads packages, resolves dependencies, and calls dpkg to perform the installation.

In short, APT decides what to install and fetches it, and dpkg does the installing.

---

## Exercise 2 — Inspect Installed Packages

**Commands**
```bash
dpkg-query -l | head -n 10
dpkg-query -W -f='${Package} ${Version} ${Status}\n' bash
dpkg -S "$(which cat)"
```

**Output**
```
<PASTE output of all three commands>
```

**Explanation**
- In `dpkg-query -l`, the status `ii` means the package is desired for install and currently installed. Each row shows name, version, architecture, and description.
- `dpkg -S` maps a file path to the package that owns it. The `cat` executable is owned by the package **<PASTE package name from dpkg -S>**.

---

## Exercise 3 — Search and Inspect Packages

**Commands**
```bash
apt search tree
apt show tree
apt-cache policy tree
```

**Output**
```
$ apt search tree
<PASTE first ~10 lines>

$ apt show tree
<PASTE>

$ apt-cache policy tree
tree:
  Installed: 2.3.1-1
  Candidate: 2.3.1-1
  Version table:
 *** 2.3.1-1 500
        500 http://archive.ubuntu.com/ubuntu resolute/universe amd64 Packages
        100 /var/lib/dpkg/status
```

**Observations**
- `apt search` matches package names and descriptions, so it returns many loosely related packages.
- `apt show` gives full metadata: version, dependencies, size, and source.
- `apt-cache policy` shows `tree` is **already installed** at 2.3.1-1, which equals the candidate version, so it is up to date. It comes from the `resolute/universe` repository. The `*** ` marker shows the installed version, and the `100 /var/lib/dpkg/status` line is the local dpkg database.

---

## Exercise 4 — Refresh the Package Index

**Command**
```bash
sudo apt update
```

**Output**
```
<PASTE output of sudo apt update>
```

**Update vs. upgrade**
- `apt update` downloads the latest package lists (metadata) from the configured repositories. It does not change installed software.
- `apt upgrade` downloads and installs newer versions of installed packages.

`update` tells APT what is available, and `upgrade` acts on it. I ran only `update`.

---

## Exercise 5 — Inspect Available Updates

**Command**
```bash
apt list --upgradable | head -20
```

**Output (first entries)**
```
Listing...
alsa-ucm-conf/resolute-updates,resolute-updates 1.2.15.3-1ubuntu1.7 all [upgradable from: 1.2.15.3-1ubuntu1.5]
bpftool/resolute-updates 7.7.0+7.0.0-42.42 amd64 [upgradable from: 7.7.0+7.0.0-38.38]
brave-browser-nightly/stable 1.101.3 amd64 [upgradable from: 1.98.36]
cloud-init-base/resolute-updates,resolute-updates 26.2-0ubuntu1~26.04.1 all [upgradable from: 26.1-0ubuntu3~26.04.1]
cloud-init/resolute-updates,resolute-updates 26.2-0ubuntu1~26.04.1 all [upgradable from: 26.1-0ubuntu3~26.04.1]
containerd.io/resolute 2.4.2-3~ubuntu.26.04~resolute amd64 [upgradable from: 2.3.5-1~ubuntu.26.04~resolute]
dnsmasq-base/resolute-updates 2.92-1ubuntu0.5 amd64 [upgradable from: 2.92-1ubuntu0.4]
docker-buildx-plugin/resolute 0.38.1-1~ubuntu.26.04~resolute amd64 [upgradable from: 0.37.1-1~ubuntu.26.04~resolute]
docker-ce-cli/resolute 5:29.9.2-1~ubuntu.26.04~resolute amd64 [upgradable from: 5:29.8.1-1~ubuntu.26.04~resolute]
docker-ce-rootless-extras/resolute 5:29.9.2-1~ubuntu.26.04~resolute amd64 [upgradable from: 5:29.8.1-1~ubuntu.26.04~resolute]
docker-ce/resolute 5:29.9.2-1~ubuntu.26.04~resolute amd64 [upgradable from: 5:29.8.1-1~ubuntu.26.04~resolute]
docker-compose-plugin/resolute 5.6.1-1~ubuntu.26.04~resolute amd64 [upgradable from: 5.5.1-1~ubuntu.26.04~resolute]
docker-model-plugin/resolute 1.2.9-1~ubuntu.26.04~resolute amd64 [upgradable from: 1.2.6-1~ubuntu.26.04~resolute]
freedownloadmanager/unknown 6.35.2.7075 amd64 [upgradable from: 6.35.0.7018]
gir1.2-adw-1/resolute-updates 1.9.1-0ubuntu0.2 amd64 [upgradable from: 1.9.1-0ubuntu0.1]
gir1.2-mutter-18/resolute-updates 50.1-0ubuntu2.5 amd64 [upgradable from: 50.1-0ubuntu2.4]
glycin-loaders/resolute-updates 2.1.5+ds-0ubuntu0.2 amd64 [upgradable from: 2.1.1+ds-0ubuntu1]
glycin-thumbnailers/resolute-updates 2.1.5+ds-0ubuntu0.2 amd64 [upgradable from: 2.1.1+ds-0ubuntu1]
gnome-shell-common/resolute-updates,resolute-updates 50.1-0ubuntu1.4 all [upgradable from: 50.1-0ubuntu1.2]
```

**Observations**
- **117 packages** were upgradable in total (see Exercise 6). Only the first 20 lines are shown above.
- The list mixes Ubuntu repository updates (`resolute-updates`) with updates from other sources: Docker (`docker-ce`, `containerd.io`), Brave (`brave-browser-nightly`), and Free Download Manager (`freedownloadmanager`, source shown as `unknown`).
- **No upgrades were installed.** `apt list --upgradable` is read-only, and no upgrade command was run.

---

## Exercise 6 — Simulate an Installation

**Command**
```bash
apt-get -s install tree
```

**Output**
```
NOTE: This is only a simulation!
      apt-get needs root privileges for real execution.
      Keep also in mind that locking is deactivated,
      so don't depend on the relevance to the real current situation!
Reading package lists...
Building dependency tree...
Reading state information...
tree is already the newest version (2.3.1-1).
Solving dependencies...
0 upgraded, 0 newly installed, 0 to remove and 117 not upgraded.
```

**Explanation**
- `-s` simulates the action, so nothing is installed, removed, or changed.
- `tree` is already installed at the newest available version (2.3.1-1), so APT proposed **no package or dependency changes**: 0 upgraded, 0 newly installed, 0 to remove.
- The 117 "not upgraded" packages are the pending updates from Exercise 5. They were not touched because I did not request an upgrade.

---

## Exercise 7 — Install and Inspect a Package

**Installation was skipped.** `tree` was already installed at version 2.3.1-1, matching the candidate version (Exercises 3 and 6). Reinstalling would change nothing, so I inspected the existing installation instead.

**Commands**
```bash
which tree
tree --version
dpkg -l tree
dpkg -S "$(which tree)"
dpkg -L tree
```

**Output**
```
<PASTE output>
```

**Verification and ownership**
- `dpkg -l tree` should show status `ii` (installed correctly).
- `dpkg -S` links `/usr/bin/tree` to the `tree` package, **<confirm from your output>**.
- `dpkg -L tree` lists every file the package installed: the binary, documentation, and man page.

---

## Independent Challenge

- **Package selected:** `<e.g. htop>`
- **Version:** `<from apt-cache policy>`
- **Commands:**
```bash
apt show <package>
apt-cache policy <package>
apt-get -s install <package>
```
- **Simulation results:** `<PASTE the "X upgraded, Y newly installed, Z to remove" line>` Dependencies proposed: `<list or none>`.
- **Decision:** `<Installed / Not installed, and why>`
- **What I learned:** Simulation with `-s` shows exactly what will change before anything is installed. `apt-cache policy` shows installed vs. candidate versions and which repository a package comes from, and `dpkg -S` / `dpkg -L` connect files to their owning packages.

---

## Troubleshooting

No errors occurred during this lab. The `apt-get -s` simulation printed a notice that it needs root for real execution and that locking is disabled. This is expected behaviour for simulations, not an error.

*(Replace this if you hit a real error, using the format: error message, cause, resolution.)*

---

## Security Considerations
- Used configured Ubuntu software repositories for `tree` (`resolute/universe`).
- Inspected package information (`apt show`, `apt-cache policy`) before any installation decision.
- Reviewed the simulated changes before deciding whether to install.
- Did not add any new third-party repositories during this lab. The system already had Docker, Brave, and Free Download Manager sources configured beforehand. These are outside the Ubuntu archive, and their updates should be trusted deliberately.
- Did not perform an automatic full-system upgrade. 117 packages remained pending.
- Did not remove existing packages during this exercise.

---

## Conclusion
APT and dpkg work together to manage software on Debian-based systems. dpkg handles the low-level work of installing, removing, and querying individual packages, and it tracks what is installed. APT sits on top of it, using repositories to find packages, resolve dependencies, and fetch updates. This lets administrators install software consistently, trace any file to its owning package, and preview changes before applying them. In this lab, the simulation confirmed that `tree` was already current and that nothing would change.

Package maintenance matters for security because most vulnerabilities are fixed through package updates. This system had 117 pending updates, including security-relevant components such as `containerd`, `docker-ce`, and `cloud-init`, and running outdated versions leaves known flaws exposed. Using signed repositories, reviewing changes before installing, and keeping the index and installed packages current reduces the attack surface. Third-party repositories deserve extra scrutiny, since they sit outside Ubuntu's security process.

---

## Further Practice
- Explore package verification using dpkg (`dpkg -V <package>`, `debsums`).
- Learn about repository configuration (`/etc/apt/sources.list.d/`, including the deb822 `.sources` format).
- Study package dependencies (`apt depends`, `apt rdepends`).
- Understand the difference between removing and purging packages (`apt remove` keeps configuration files, `apt purge` deletes them too).
- Explore Snap package management (`snap list`, `snap find`, `snap info`).
