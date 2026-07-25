# Chapter 2: Manage Software

## Objective

Learn how software is managed on Red Hat Enterprise Linux using RPM, DNF, repositories, and Flatpak.

---

# RPM vs DNF

## RPM (Red Hat Package Manager)

RPM is the low-level package management system in RHEL.

It can:

- Install RPM packages
- Remove packages
- Query installed packages
- Verify packages

RPM does **not** resolve dependencies or download packages from repositories.

### Syntax

```bash
rpm [options]
```

---

## DNF (Dandified Yum)

DNF is the high-level package manager that uses RPM underneath.

DNF can:

- Search packages
- Install software
- Remove software
- Update software
- Resolve dependencies
- Access repositories
- Manage package transactions

---

# RPM vs DNF

| RPM | DNF |
|------|-----|
| Low-level package manager | High-level package manager |
| Works directly with RPM packages | Uses repositories |
| No dependency resolution | Resolves dependencies automatically |
| No repository support | Supports repositories |
| Uses RPM database | Uses RPM underneath |

---

# Repository

A repository is a centralized storage location that contains RPM packages and metadata.

DNF communicates with repositories whenever software is searched, installed, updated, or removed.

---

# Repository Metadata

Repository metadata contains information required by DNF.

It includes:

- Package names
- Versions
- Dependencies
- Architecture
- Checksums
- Repository information

DNF downloads metadata first before performing package operations.

---

# BaseOS Repository

Contains the core operating system packages.

Examples:

- Kernel
- Bash
- Core utilities
- System libraries

These packages form the operating system.

---

# AppStream Repository

Contains user-space applications and development software.

Examples:

- Databases
- Programming languages
- Web servers
- Editors
- Runtime environments

AppStream evolves independently from BaseOS.

---

# DNF Transaction Workflow

Every install, remove, reinstall, or update is performed as a transaction.

Workflow:

1. Read repository metadata
2. Find requested package
3. Resolve dependencies
4. Build transaction
5. Show transaction summary
6. Ask for confirmation
7. Execute transaction
8. Update RPM database

---

# Package Queries

## Check if a package is installed

```bash
rpm -q package
```

Example

```bash
rpm -q tmux
```

---

## List files installed by a package

```bash
rpm -ql package
```

Example

```bash
rpm -ql openssh-server
```

---

## Find which package owns a file

```bash
rpm -qf /path/to/file
```

Example

```bash
rpm -qf /usr/bin/passwd
```

---

# Repository Commands

## List enabled repositories

```bash
dnf repolist
```

---

## Search packages

```bash
dnf search keyword
```

Example

```bash
dnf search nginx
```

---

## Package information

```bash
dnf info package
```

Example

```bash
dnf info httpd
```

---

# Install Packages

```bash
sudo dnf install package
```

Example

```bash
sudo dnf install tree
```

DNF automatically resolves dependencies.

---

# Remove Packages

```bash
sudo dnf remove package
```

Example

```bash
sudo dnf remove tree
```

DNF checks dependencies before removing packages.

---

# Reinstall Packages

Reinstalls an already installed package.

```bash
sudo dnf reinstall package
```

Example

```bash
sudo dnf reinstall tmux
```

Useful when package files become corrupted.

---

# Update Packages

Update every installed package

```bash
sudo dnf update
```

Update one package

```bash
sudo dnf update bash
```

DNF compares installed versions against repository versions before performing updates.

---

# Local RPM Installation

Install a local RPM file using DNF

```bash
sudo dnf install ./package.rpm
```

or

```bash
sudo dnf localinstall package.rpm
```

Using DNF is preferred because it resolves dependencies automatically.

RPM can also install local packages:

```bash
sudo rpm -ivh package.rpm
```

However, RPM does not resolve dependencies.

---

# Configure RPM Repositories

Repository configuration files are stored in

```text
/etc/yum.repos.d/
```

Repository files use the `.repo` extension.

Example

```text
example.repo
```

Common repository options

- name
- baseurl
- enabled
- gpgcheck
- gpgkey

List enabled repositories

```bash
dnf repolist
```

---

# Flatpak

Flatpak is a package management system for desktop applications.

Applications run inside isolated sandboxes.

Flatpak applications are independent of traditional RPM packages.

---

# Configure Flatpak Repository

Add Flathub

```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

List configured remotes

```bash
flatpak remotes
```

---

# Search Flatpak Packages

```bash
flatpak search package
```

Example

```bash
flatpak search vlc
```

---

# Install Flatpak Package

```bash
flatpak install flathub package-name
```

Example

```bash
flatpak install flathub org.videolan.VLC
```

---

# Remove Flatpak Package

```bash
flatpak uninstall package-name
```

Example

```bash
flatpak uninstall org.videolan.VLC
```

---

# Update Flatpak Packages

```bash
flatpak update
```

---

# Key Takeaways

- RPM is the low-level package manager.
- DNF is the high-level package manager built on top of RPM.
- DNF resolves dependencies and manages repositories.
- Repository metadata allows DNF to locate and resolve packages.
- BaseOS contains core operating system packages.
- AppStream contains user applications and development software.
- Every DNF operation is executed as a transaction.
- Prefer DNF over RPM for package installation.
- Repository files are stored in `/etc/yum.repos.d/`.
- Flatpak manages sandboxed desktop applications independently of RPM.
