# Network Load Balancing Lab

## Overview

This project demonstrates the deployment and configuration of a highly available web infrastructure using Windows Server Network Load Balancing (NLB). The environment consists of two IIS web servers configured within an NLB cluster and managed through Active Directory Domain Services (AD DS).

The objective was to create a fault-tolerant web environment capable of distributing client requests across multiple servers while maintaining service availability.

## Key Achievements

- Built a two-node Network Load Balancing cluster
- Configured Active Directory Domain Services
- Deployed IIS web services across multiple servers
- Implemented DNS and host-based name resolution
- Verified successful traffic distribution and high availability

---

## Table of Contents

- [Technologies Used](#technologies-used)
- [Project Objectives](#project-objectives)
- [Network Architecture](#network-architecture)
- [Server Configuration](#server-configuration)
- [Implementation Steps](#implementation-steps)
  - [1. Server Preparation](#1-server-preparation)
  - [2. Service Installation](#2-service-installation)
  - [3. Active Directory Configuration](#3-active-directory-configuration)
  - [4. Network Load Balancing](#4-network-load-balancing)
  - [5. IIS Deployment](#5-iis-deployment)
  - [6. DNS Resolution](#6-dns-resolution)
- [Results](#results)
- [Skills Demonstrated](#skills-demonstrated)
- [Screenshots](#screenshots)
- [Documentation](#documentation)
- [Lessons Learned](#lessons-learned)

## Technologies Used

- Windows Server 2019
- Internet Information Services (IIS)
- Network Load Balancing (NLB)
- Active Directory Domain Services (AD DS)
- DNS
- TCP/IP Networking
- VirtualBox / VMware (Lab Environment)

---

## Project Objectives

- Configure two Windows Server hosts
- Assign static IP addresses
- Install and configure IIS
- Install and configure Network Load Balancing
- Deploy Active Directory Domain Services
- Promote a server to Domain Controller
- Join additional servers to the domain
- Create an NLB cluster
- Deploy a test website on both servers
- Verify load-balanced access through a shared cluster address

---

## Network Architecture

```text
                     Client
                        │
                        ▼
                192.168.50.200
             (NLB Cluster Address)
                        │
        ┌───────────────┴───────────────┐
        │                               │
        ▼                               ▼
+----------------+            +----------------+
|  NLB-Server1   |            |  NLB-Server2   |
| IIS Web Server |            | IIS Web Server |
| Domain Control |            | Domain Member  |
+----------------+            +----------------+

```

---

## Server Configuration

| Setting | NLB-Server1 | NLB-Server2 |
|----------|------------|------------|
| Hostname | NLB-server1 | NLB-server2 |
| Role | Domain Controller | Domain Member |
| Services | IIS, NLB, AD DS | IIS, NLB |
| Primary IP | 192.168.50.114 | 192.168.50.117 |
| Secondary IP | 192.168.50.115 | 192.168.50.118 |

### Cluster Configuration

| Setting | Value |
|-----------|--------|
| Cluster IP | 192.168.50.200 |
| Cluster Name | www.nlbcluster.com |
| Mode | Multicast |

---

## Implementation Steps

### 1. Server Preparation

- Generated unique SIDs using Sysprep
- Completed OOBE configuration
- Renamed servers
- Configured static networking

### 2. Service Installation

Installed:

- IIS Web Server
- Network Load Balancing Feature
- Active Directory Domain Services

### 3. Active Directory Configuration

- Created a new forest
- Promoted NLB-server1 to Domain Controller
- Created domain:

```text
nlbserver.local
```

- Joined NLB-server2 to the domain

### 4. Network Load Balancing

Created an NLB cluster using:

```text
192.168.50.200
```

Added:

- NLB-server1
- NLB-server2

Verified both hosts reached a **Converged** state.

### 5. IIS Deployment

Created a custom website on both servers:

```html
<html>
<head>
<title>NLB Server</title>
</head>
<body>
<h1>You have reached NLB-server1.</h1>
</body>
</html>
```

Configured:

- Website bindings
- Physical paths
- Default documents

### 6. DNS Resolution

Modified the hosts file:

```text
192.168.50.200    www.nlbcluster.com
```

---

## Results

Successfully deployed:

- Active Directory Domain
- Two IIS Web Servers
- Network Load Balancing Cluster
- Shared Cluster IP Address
- Website accessible through:

```text
www.nlbcluster.com
```

The cluster distributed requests between both backend web servers while maintaining service availability.

---

## Skills Demonstrated

- Windows Server Administration
- Active Directory Management
- Network Load Balancing
- IIS Configuration
- DNS Configuration
- Static IP Networking
- High Availability Design
- Infrastructure Deployment
- Troubleshooting and Validation

---

## Screenshots

### Domain Controller Configuration

<img width="1225" height="926" alt="image" src="https://github.com/user-attachments/assets/befc6573-33cc-4625-ab7d-4ed20c9dd823" />

*Source: Report Page 53*

### NLB Cluster

<img width="1045" height="785" alt="image" src="https://github.com/user-attachments/assets/5cb8aa51-bbc2-479b-a609-266616645d7c" />

*Source: Report Page 61*

### IIS Website

<img width="1227" height="925" alt="image" src="https://github.com/user-attachments/assets/a1fe67ef-38ea-4946-a248-9e5581b23e46" />

*Source: Report Page 78*

### Successful Load Balancing Test

<img width="1227" height="925" alt="image" src="https://github.com/user-attachments/assets/6634f5b6-d2e6-4687-b6a2-5fcdcb61e929" />

*Source: Report Page 84*

<img width="1223" height="925" alt="image" src="https://github.com/user-attachments/assets/e7fe0bd0-599d-4193-9f17-186eb2b76b76" />

*Source: Report Page 85*

---

## Documentation

A complete step-by-step implementation guide is included in:

```text
documentation/Network_Load_Balancing.pdf
```

---

## Lessons Learned

This project provided practical experience with:

- Building highly available web infrastructure
- Managing Windows Server roles and features
- Configuring Active Directory environments
- Implementing Network Load Balancing
- Deploying and validating IIS web services
- Troubleshooting enterprise networking issues

---

## Author

**Jarred Ward**

Windows Server • Active Directory • IIS • Network Load Balancing • System Administration
