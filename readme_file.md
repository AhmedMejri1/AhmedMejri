# OpenPBS Installer

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![OS Support](https://img.shields.io/badge/OS-Ubuntu%20|%20RHEL%20|%20Rocky%20|%20CentOS-green.svg)
![Architecture](https://img.shields.io/badge/arch-x86__64%20|%20arm64-lightgrey.svg)

A comprehensive installation script for OpenPBS (Portable Batch System) that automates the download, compilation, and configuration process across multiple Linux distributions.

## ✨ Features

- **Multi-Distribution Support**: Ubuntu 20.04+, RHEL/CentOS 7/8/9, Rocky Linux 8/9, AlmaLinux 8/9
- **Architecture Support**: x86_64 and arm64
- **Flexible Node Types**: Server, compute, or combined installations
- **Accounting Support**: Optional PostgreSQL integration for job accounting
- **Interactive & Non-Interactive**: Both guided setup and automated deployment
- **Source Compilation**: Always uses latest features from OpenPBS master branch
- **Production Ready**: Includes proper security configurations and service management

## 🚀 Quick Start

### One-Line Installation

```bash
# Download and run installer
sudo bash -c "$(wget -qO- https://raw.githubusercontent.com/yourusername/OpenPBS-Installer/main/pbs_install.sh)"
```

### Standard Installation

```bash
# Clone repository
git clone https://github.com/yourusername/OpenPBS-Installer.git
cd OpenPBS-Installer

# Make executable
chmod +x pbs_install.sh

# Run installer
sudo ./pbs_install.sh
```

## 📋 Prerequisites

### System Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| **Server Node** | 2GB RAM, 20GB disk | 4GB RAM, 50GB disk |
| **Compute Node** | 1GB RAM, 10GB disk | 2GB RAM, 20GB disk |
| **Network** | 100 Mbps | 1 Gbps |

### Supported Operating Systems

- **Ubuntu**: 20.04, 22.04, 24.04
- **RHEL**: 7, 8, 9
- **CentOS**: 7, 8, 9  
- **Rocky Linux**: 8, 9
- **AlmaLinux**: 8, 9

## 🔧 Usage

### Interactive Installation

```bash
sudo ./pbs_install.sh
```

The script will guide you through:
1. Node type selection (server/compute/both)
2. Cluster configuration
3. Optional accounting setup
4. Service configuration

### Non-Interactive Installation

#### PBS Server Node
```bash
sudo ./pbs_install.sh \
    --node-type=server \
    --cluster-name=mycluster \
    --without-interaction
```

#### PBS Compute Node
```bash
sudo ./pbs_install.sh \
    --node-type=compute \
    --server-hostname=pbsserver \
    --without-interaction
```

#### Server with Accounting
```bash
sudo ./pbs_install.sh \
    --node-type=server \
    --enable-accounting \
    --install-postgres \
    --postgres-password=securepass \
    --without-interaction
```

### Advanced Options

```bash
# Install specific version
export PBS_VERSION=v23.06.06
sudo ./pbs_install.sh --node-type=server

# Custom installation path
export PBS_PREFIX=/usr/local/pbs
sudo ./pbs_install.sh --node-type=server

# Force reinstallation
sudo ./pbs_install.sh --force-reinstall --node-type=server
```

## 📝 Command Line Options

| Option | Description | Example |
|--------|-------------|---------|
| `--node-type=TYPE` | Node type: server, compute, or both | `--node-type=server` |
| `--server-hostname=HOST` | PBS server hostname | `--server-hostname=pbsmaster` |
| `--cluster-name=NAME` | Cluster identifier | `--cluster-name=research-cluster` |
| `--enable-accounting` | Enable PostgreSQL accounting | `--enable-accounting` |
| `--postgres-password=PASS` | PostgreSQL password | `--postgres-password=mypass` |
| `--install-postgres` | Install PostgreSQL server | `--install-postgres` |
| `--force-reinstall` | Overwrite existing installation | `--force-reinstall` |
| `--without-interaction` | Non-interactive mode | `--without-interaction` |

## 🏗️ Architecture Examples

### Single-Node Setup (Development/Testing)
```bash
sudo ./pbs_install.sh --node-type=both --cluster-name=dev-cluster
```

### Multi-Node Cluster
```bash
# On server node (pbsmaster)
sudo ./pbs_install.sh --node-type=server --cluster-name=prod-cluster

# On compute node 1 (node01)
sudo ./pbs_install.sh --node-type=compute --server-hostname=pbsmaster

# On compute node 2 (node02)  
sudo ./pbs_install.sh --node-type=compute --server-hostname=pbsmaster
```

### High-Availability Setup
```bash
# Primary server with accounting
sudo ./pbs_install.sh \
    --node-type=server \
    --cluster-name=ha-cluster \
    --enable-accounting \
    --install-postgres \
    --postgres-password=strongpassword
```

## 🔍 Post-Installation

### Verify Installation

```bash
# Check PBS server status
qstat -B

# List compute nodes
pbsnodes -a

# View queues
qstat -Q
```

