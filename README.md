*This project has been created as part of the 42 curriculum by fda-cruz*

## Description

NetPractice is a networking project where the goal is to configure a series of progressively more complex virtual network topologies.

The project focuses on understanding how devices communicate through IPv4 addressing, subnetting, routing and gateways until all hosts are able to exchange packets successfully.

## Instructions

### Execution

Run the interface:

```bash
./net_practice/run.sh
```

If the script is unavailable or does not work on your system, you can launch the interface manually:

```bash
python3 -m http.server 49242
```

Then open `http://localhost:49242` in your browser.

### Solve Levels

Enter your login in the interface. You will automatically start at Level 1. Complete each level and use **Check again** until all objectives are validated. Repeat the process until all 10 levels are completed.

### Export Configurations

Use **Get my config** after each Level is solved.
Save all exported files at the root of the repository.

### Submission Requirements

The repository root must contain the ten exported configuration files (one for each Level).

## Technical Overview

### Network Communication

A **network** is a group of two or more devices connected in a way that allows them to exchange information. This information is transmitted as **packets**, small units of data, sent from one device to another.

In order to transfer data from one point to another across a network, many different types of protocols exist to ensure access, transport, security and stability.

### TCP/IP Model

To standardize network communication, layered network models were introduced. Each layer is responsible for a specific aspect of communication and interacts only with the layers directly above and below it.

The **OSI**, **Open Systems Interconnection**, model defines seven layers and is widely used as a conceptual framework for understanding how networks operate.

However, real-world networks are based on the simpler **TCP/IP** model, which combines the responsibilities of the OSI model into four layers.

| OSI Model    | TCP/IP Model |
| ------------ | ------------ |
| Application  | Application  |
| Presentation | Application  |
| Session      | Application  |
| Transport    | Transport    |
| Network      | Internet     |
| Data Link    | Link         |
| Physical     | Link         |

**TCP/IP** comes from its two core protocols:
- **Transmission Control Protocol (TCP)** is a communication standard protocol that enables devices to communicate with each other. It's responsible for ensuring that data is delivered reliably, in the correct order and without loss.
- **Internet Protocol (IP)** provides the addressing system that uniquely identifies devices on a network and allows packets to be routed to their destination.

**TCP** and **IP** are not the same thing, but rather two separate protocols that work together in order ensure data transfer between different devices. 

Since this project focuses on network configuration rather than data transmission reliability, the project primarily explores the concepts related to **IP** addressing and routing.

The first concept to understand is the addressing system used by **IP**.

### IPv4 Addressing

There are two different version of IP Addresses: **IPv4** and **IPv6**. For the purpose of this project, we will only need to know about the first one.

An **IP Address** is a 32 bit number assigned to a device connected to a network. It's divided into four 8 bit blocks, known as **octets**, separated by dots. Each of these range from `0` to `255`, in binary `00000000` to `11111111`.

```text
Decimal: 192.168.1.42
Binary:  11000000.10101000.00000001.00101010
```
---

Although **IP Addresses** are commonly written in decimal notation, understanding their binary representation is essential. Every bit carries information used to determine both the network a device belongs to and the device's identity within that network. They are logically divided into two parts:
-  **Network ID**: identifies the network to which the device belongs.
- **Host ID**: uniquely identifies a device within that network.

Devices can communicate directly only when they belong to the same network, meaning they share the same **Network ID** while having different **Host IDs**.

The boundary between these two portions is determined by the **Subnet Mask**, which specifies which bits belong to the network and which belong to the host.

### Subnet Masks

In order to identify which part of the full **IP Address** corresponds to the **Network ID** and which corresponds to the **Host ID**, we must apply to it a **Network Mask** also called **Subnet Mask**.

A **Subnet Mask** is also a 32 bit number divided into four **octets**. It's purpose is to indicate which bits belong to the **Network ID** and which belong to the **Host ID**.

A bit set to **1** indicates that the corresponding bit of the **IP address** belongs to the **Network ID**, while a bit set to **0** indicates that it belongs to the **Host ID**. **Subnet Masks** always contain contiguous `1`s followed by contiguous `0`s. Once the first `0` appears, every following bit must also be `0`.

To determine the **Network ID** of an **IP Address**, a bitwise `AND` operation is performed between the **IP Address** and the **Subnet Mask**. The result of the operation is the **Network ID**.

```text
IP Address:  192.168.1.42
Binary:      11000000.10101000.00000001.00101010

Subnet Mask: 255.255.255.0
Binary:      11111111.11111111.11111111.00000000

-------------------------------------------

Binary:      11000000.10101000.00000001.00000000
Network ID:  192.168.1.0
```

In this example, the first **24 bits** are identified by the **Subnet Mask** as the **Network ID**, while the remaining **8 bits** represent the **Host ID**.

Knowing the **Network ID** allows a device to determine whether another host belongs to the same network or to a different one. Devices within the same network can communicate directly, while communication with devices on another network requires a **Router**.

Writing **Subnet Masks** in their full decimal form is not always convenient. For this reason, a shorter representation called **CIDR Notation** is commonly used.

### CIDR Notation



### Network and Broadcast Addresses



### Switches



### Routers



### Default Gateways



### Routing Tables



### Packet Forwarding



## Resources



### Use of AI
