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

### IPv4 addressing

There are two different version of IP Addresses: **IPv4** and **IPv6**. For the purpose of this project, we will only need to know about the first one.

### Subnet masks



### CIDR notation



### Network and broadcast addresses



### Switches



### Routers



### Default gateways



### Routing tables



### Packet Forwarding



## Resources



### Use of AI
