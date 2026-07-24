# Chapter 02 - Manage Software

## Overview

Manage software using RPM and DNF.

### Exam Objectives

- Configure access to RPM repositories
- Install and remove RPM software packages
- Configure access to Flatpak repositories
- Install and remove Flatpak software packages

---

## Package Management Concepts

### RPM

- Low-level package manager.
- Works with installed RPM packages.
- Maintains the local RPM database.
- Does not resolve dependencies.
- Does not download packages.

### DNF

- High-level package manager.
- Searches repositories.
- Resolves dependencies.
- Downloads packages.
- Verifies package signatures.
- Uses RPM to perform package installation.

### DNF vs RPM

| DNF | RPM |
|------|-----|
| High-level package manager | Low-level package manager |
| Resolves dependencies | Does not resolve dependencies |
| Downloads packages | Does not download packages |
| Searches repositories | Queries installed packages |
| Uses RPM internally | Performs package operations |

---

## Repository Concepts

### Repository

- Collection of RPM packages.
- Contains repository metadata.
- Packages are installed from repositories.

### Repository Metadata

- Package names
- Versions
- Dependencies
- Checksums
- Signatures

---

## Repository Commands

### List Repositories

- Displays enabled repositories.

- **Syntax**

```bash
dnf repolist
```

- **Example**

```bash
dnf repolist
```

- **Notes**

Displays repositories such as BaseOS and AppStream.

---

### Search Packages

- Search repositories for packages.

- **Syntax**

```bash
dnf search <package>
```

- **Examples**

```bash
dnf search tmux
dnf search wget
dnf search tree
```

- **Notes**

Searches repositories, not installed packages.

---

### Package Information

- Show package details.

- **Syntax**

```bash
dnf info <package>
```

- **Example**

```bash
dnf info tmux
```

- **Notes**

If installed:

```
Installed Packages
```

If available but not installed:

```
Available Packages
```

---

## RPM Query Commands

### Check Installed Package

- Determine whether a package is installed.

- **Syntax**

```bash
rpm -q <package>
```

- **Example**

```bash
rpm -q tmux
```

---

### List Files Installed by a Package

- Lists every file belonging to an installed package.

- **Syntax**

```bash
rpm -ql <package>
```

- **Example**

```bash
rpm -ql tmux
```

---

### Find Package Owning a File

- Determine which package owns a file.

- **Syntax**

```bash
rpm -qf <file>
```

- **Example**

```bash
rpm -qf /usr/bin/tmux
```

---

## Installing Packages

### Install Package

- Install a package from configured repositories.

- **Syntax**

```bash
dnf install <package>
```

- **Example**

```bash
dnf install tmux
```

---

## DNF Transaction Workflow

When running:

```bash
dnf install tmux
```

DNF performs the following steps:

1. Contact Subscription Manager.
2. Read repository metadata.
3. Resolve dependencies.
4. Build the transaction.
5. Download RPM packages.
6. Perform transaction check.
7. Perform transaction test.
8. Call RPM.
9. Install package files.
10. Run package scriptlets.
11. Update RPM database.
12. Complete the transaction.

---

## Download Size vs Installed Size

### Download Size

Compressed RPM downloaded from repository.

### Installed Size

Actual disk space consumed after extraction.

---

## Important Notes

- Repository metadata is not the package itself.
- RPM never downloads dependencies.
- DNF uses RPM internally.
- Think in terms of questions:

| Question | Command |
|----------|---------|
| Is package installed? | `rpm -q` |
| What files belong to package? | `rpm -ql` |
| Which package owns this file? | `rpm -qf` |
| Is package available? | `dnf search` |
| Package details? | `dnf info` |

---

## Progress

### Completed

- RPM vs DNF
- Repository concepts
- Repository metadata
- BaseOS vs AppStream
- dnf repolist
- dnf search
- dnf info
- rpm -q
- rpm -ql
- rpm -qf
- dnf install
- DNF transaction workflow

### Remaining

- dnf remove
- dnf reinstall
- dnf update
- Local RPM installation
- Configure RPM repositories
- Configure Flatpak repositories
- Install/remove Flatpak packages
