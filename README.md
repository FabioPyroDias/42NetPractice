*This project has been created as part of the 42 curriculum by fda-cruz*

## Description

NetPractice is a networking project where the goal is to configure a series of progressively more complex virtual network topologies.

Each level presents an incomplete network configuration with one or more communication goals. The objective is to correctly configure **IP Addresses**, **Subnet Masks**, **Default Gateways** and **Routing Tables** until every communication goal is successfully achieved.

No commands or configuration files are edited directly. Instead, all configuration is performed through the graphical interface provided by NetPractice.

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

There are two different version of **IP Addresses**: **IPv4** and **IPv6**. For the purpose of this project, we will only need to know about the first one.

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

The subnet mask not only separates the **Network ID** from the **Host ID**, but also determines the size of the network.
A mask with more bits assigned to the **Network ID** leaves fewer bits available for the **Host ID**, reducing the number of devices that can exist within the same network. Conversely, assigning fewer bits to the **Network ID** leaves more bits available for hosts, increasing the network's capacity.

For this reason, choosing an appropriate subnet mask is essential when designing a network, as it directly determines how many devices can be connected to each subnet.

Writing **Subnet Masks** in their full decimal form is not always convenient. For this reason, a shorter representation called **CIDR Notation** is commonly used.

### CIDR Notation

Instead of writing the entire subnet mask, **CIDR**, **Classless Inter-Domain Routing**, specifies only the number of consecutive bits that belong to the **Network ID**.

```text
Decimal: 255.255.255.0
Binary: 11111111.11111111.11111111.00000000
```

Since the first **24 bits** are set to `1`, the same subnet mask can be written as:

```text
/24
```

Likewise:

```text
Subnet Mask: 255.255.240.0
Binary:      11111111.11111111.11110000.00000000
CIDR:        /20
```

Here, the first **20 bits** belong to the **Network ID**, while the remaining **12 bits** belong to the **Host ID**.

**CIDR Notation** is simply a shorter way of writing a **Subnet Mask**. Both of the following representations describe exactly the same network:

```text
IP Address:   193.168.1.42
Subnet Mask:  255.255.255.0
CIDR:         193.168.1.42/24
```

Using **CIDR Notation** also makes it easier to determine how many addresses are available within a subnet. A larger prefix means more bits are reserved for the **Network ID**, leaving fewer bits available for hosts.

| CIDR |   Subnet Mask   | Total Addresses | Usable Hosts  |
|------|-----------------|:----------------|:--------------|
| /30  | 255.255.255.252 | 4               | 2             |
| /29  | 255.255.255.248 | 8               | 6             |
| /28  | 255.255.255.240 | 16              | 14            |
| /27  | 255.255.255.224 | 32              | 30            |
| /26  | 255.255.255.192 | 64              | 62            |
| /25  | 255.255.255.128 | 128             | 126           |
| /24  | 255.255.255.0   | 256             | 254           |
| /23  | 255.255.254.0   | 512             | 510           |
| /22  | 255.255.252.0   | 1,024           | 1,022         |
| /21  | 255.255.248.0   | 2,048           | 2,046         |
| /20  | 255.255.240.0   | 4,096           | 4,094         |
| /19  | 255.255.224.0   | 8,192           | 8,190         |
| /18  | 255.255.192.0   | 16,384          | 16,382        |
| /17  | 255.255.128.0   | 32,768          | 32,766        |
| /16  | 255.255.0.0     | 65,536          | 65,534        |
| /15  | 255.254.0.0     | 131,072         | 131,070       |
| /14  | 255.252.0.0     | 262,144         | 262,142       |
| /13  | 255.248.0.0     | 524,288         | 524,286       |
| /12  | 255.240.0.0     | 1,048,576       | 1,048,574     |
| /11  | 255.224.0.0     | 2,097,152       | 2,097,150     |
| /10  | 255.192.0.0     | 4,194,304       | 4,194,302     |
| /9   | 255.128.0.0     | 8,388,608       | 8,388,606     |
| /8   | 255.0.0.0       | 16,777,216      | 16,777,214    |
| /7   | 254.0.0.0       | 33,554,432      | 33,554,430    |
| /6   | 252.0.0.0       | 67,108,864      | 67,108,862    |
| /5   | 248.0.0.0       | 134,217,728     | 134,217,726   |
| /4   | 240.0.0.0       | 268,435,456     | 268,435,454   |
| /3   | 224.0.0.0       | 536,870,912     | 536,870,910   |
| /2   | 192.0.0.0       | 1,073,741,824   | 1,073,741,822 |
| /1   | 128.0.0.0       | 2,147,483,648   | 2,147,483,646 |
| /0   | 0.0.0.0         | 4,294,967,296   | 4,294,967,294 |

### Subnetting

One of the main purposes of **Subnet Masks** is to divide a larger network into multiple smaller networks, known as **Subnets**.

A `/24` **Subnet** reserves **24 bits** for the **Network ID**, leaving **8 bits** for hosts. This provides **256 total addresses**.

Suppose we want to split this network into two equal sized **Subnets**. By borrowing one additional bit from the **Host ID**, the **Subnet Mask** becomes `/25`.

```text
Subnet Mask: 255.255.255.0
CIDR:        /24
----------------------------
CIDR:        /25
Subnet Mask: 255.255.255.128
```

The additional bit is now part of the **Network ID**, leaving only **7 bits** available for the **Host ID**.
Since the **Host ID** now consists of **7 bits**, each **Subnet** contains **128 IP Addresses**.

```text
Subnet 1
IP Address:    192.168.1.0/25
IP Range:      192.168.1.0 - 192.168.1.127

Subnet 2
IP Address:    192.168.1.128/25
IP Range:      192.168.1.128 - 192.168.1.255
```

Increasing the CIDR prefix creates more subnets but reduces the number of available hosts in each subnet. Decreasing the prefix has the opposite effect, allowing more hosts to exist within the same network.

Of those **128 IP Address**, only 126 can be assigned to hosts. The first and last addresses of every **Subnet** are reserved and cannot be assigned to hosts.
These special addresses are known as the **Network Address** and the **Broadcast Address**.

### Network and Broadcast Addresses

Every subnet reserves two IP addresses that cannot be assigned to hosts. The **Network Address**, which identifies the subnet itself, always corresponds to the first address in the subnet. The **Broadcast Address**, which is always the last address in the subnet, is used to send packets to every host within the subnet simultaneously.

For example, the **Subnet** `192.168.1.0/25` contains **128 total IP addresses**, ranging from `192.168.1.0` to `192.168.1.127`.

```text
Network Address:   192.168.1.0
Usable Hosts:      192.168.1.1 - 192.168.1.126
Broadcast Address: 192.168.1.127
```

Because these two addresses have special purposes, they cannot be assigned to individual hosts. As a result, a `/25` **Subnet** provides **128 total IP Addresses**, but only **126** are usable by devices.

### Switches

A **Switch** is a network device that connects multiple devices within the same **Local Area Network**, **LAN**, allowing them to communicate directly with one another.This device forwards packets only to the device for which they are intended. It does this by maintaining a **MAC Address Table**, which maps each connected device's **MAC Address** to one of its physical ports.

A **MAC Address** is a unique hardware identifier assigned to a **Network Interface**.

Unlike **IP Addresses**, which identify a device's location within a network, **MAC Addresses** identify the physical **Network Interface** itself.

A **Network Interface** represents a physical or virtual connection between a device and a network. Each interface has its own **IP Address** and belongs to a specific **Subnet**.

Since a **Switch** operates within a single network, it does not modify **IP Addresses**, perform routing or connect different **Subnets** together. Its only responsibility is to forward **packets** between devices that already belong to the same network.

For example, the following devices belong to the same **Subnet** and are connected to the same **Switch**:

```text
Host A: 192.168.1.10/24
Host B: 192.168.1.20/24
Host C: 192.168.1.30/24
```

If one of the devices needs to communicate with a host in a different **Subnet**, the **packet** must be sent to a **Router** instead.

### Routers

A **Router** is a device responsible for connecting different **Networks** or **Subnets**.

When a host wants to send a **packet**, it first determines whether the destination belongs to the same **Subnet** by comparing both **Network IDs**.

If both devices belong to the same **Subnet**, the **packet** is sent directly through a **Switch**.
If the destination belongs to a different **Subnet**, the **packet** must be forwarded to a **Router**, which decides where to send it next.

Consider the following example:

```text
Host A: 192.168.1.10/24
Host B: 192.168.2.20/24
```

Although both hosts use the same **Subnet Mask**, `/24`, they belong to different network:

```text
Host A Network ID: 192.168.1.0
Host B Network ID: 192.168.2.0
```

Since their **Network IDs** are different, they cannot communicate directly. Instead, **Host A** sends the **packet** to a **Router**, which forwards it to the destination network.

Routers maintain information about the networks they can reach and use this information to determine the best path for forwarding **packets**. This information is stored in a **Routing Table**, which will be discussed in a later section.

### Default Gateways

A **Default Gateway** is the **IP Address** of the **Router** that a host uses whenever the destination belongs to a different network.

When a host needs to communicate with a device outside its own **Subnet**, it sends the **packet** to its **Default Gateway** instead of directly to the destination.

For example, consider the following network:

```text
Host A
IP Address:       192.168.1.10/24
Default Gateway:  192.168.1.1

Destination:
192.168.2.20/24
```

In this example, **Host A** wants to communicate with `192.168.2.20`. Since the destination belongs to a different subnet, **Host A** cannot send the **packet** directly.

Instead, it forwards the **packet** to its **Default Gateway**, `192.168.1.1`. From that point on, the **Router** becomes responsible for forwarding the **packet** towards its final destination.

The **Router** then determines the next destination by consulting its **Routing Table**.

### Routing Tables

A **Routing Table** is a table maintained by a **Router** that contains information about the networks it can reach and where **packets** should be forwarded.

Each entry typically contains:

- A **Destination Network**.
- A **Subnet Mask** or **CIDR** prefix.
- The **Next Hop**, indicating where the **packet** should be sent next.

For example:

```text
Destination Network + CIDR => Next Hop
--------------------------------------
192.168.1.0/24             => Direct
192.168.2.0/24             => Direct
0.0.0.0/0                  => 192.168.2.1
```

A route marked as **Direct** indicates that the **Destination Network** is directly connected to one of the **Router**'s interfaces. In this case, the **Router** can deliver the **packet** to the **Destination Network** without relying on another **Router**.

When a **Router** receives a **packet**, it compares the destination **IP Address** against the entries in its **Routing Table**. If a matching entry is found, the **Router** forwards the **packet** through the corresponding interface or to the specified **Next Hop**.

For example, if the destination **IP Address** is `192.168.2.35`, the **Router** matches it against the entry `192.168.2.0/24`. Since this route is marked as **Direct**, the **packet** is forwarded directly through the **Router**'s interface connected to that network.

If multiple entries match the destination, the **Router** always selects the **most specific route**, meaning the entry with the longest **CIDR** prefix.

If no specific route matches, the **Router** uses the **Default Route**, `0.0.0.0/0`, if one is configured.

### Packet Forwarding

**Packet Forwarding** is the process of moving a **packet** from its source to its destination across one or more networks.

Suppose **Host A**, `192.168.1.10/24`, wants to communicate with **Host B** `192.168.2.20/24`.

1. **Host A** determines that the destination belongs to a different **Subnet** by comparing their **Network IDs**.
2. Since the destination is outside its local network, the **packet** is sent to the configured **Default Gateway**.
3. The **Router** receives the **packet** and consults its **Routing Table**.
4. The **Router** selects the best matching route and forwards the **packet** towards the **Destination Network**.
5. Once the **packet** reaches the **Destination Network**, it is delivered through a **Switch** to **Host B**.

Throughout this process, each network device performs a specific role:

- **Hosts** generate and receive **packets**.
- **Switches** forward **packets** within the same **Subnet**.
- **Routers** forward **packets** between different networks.
- **Routing Tables** determine where **packets** should be forwarded next.
- **Default Gateways** provide hosts with a path to networks outside their own.

Understanding this forwarding process is the key objective of **NetPractice**, as every exercise requires configuring the network so that **packets** can successfully travel from their source to their destination.

### Project Structure
```text
.
├── level1.json
├── level2.json
├── level3.json
├── level4.json
├── level5.json
├── level6.json
├── level7.json
├── level8.json
├── level9.json
├── level10.json
└── README.md
```

## Resources

[Layers of OSI Model](https://www.geeksforgeeks.org/computer-networks/open-systems-interconnection-model-osi/)

[TCP/IP Model](https://www.geeksforgeeks.org/computer-networks/tcp-ip-model/)

[Role of Subnet Mask](https://www.geeksforgeeks.org/computer-networks/role-of-subnet-mask/)

[Classless Inter Domain Routing (CIDR)](https://www.geeksforgeeks.org/computer-networks/classless-inter-domain-routing-cidr/)

[IP Addressing and CIDR](https://www.geeksforgeeks.org/devops/ip-addressing-and-cidr/)

[Introduction to Subnetting](https://www.geeksforgeeks.org/computer-networks/introduction-to-subnetting/)

[What is a Network Switch and How Does It Work?](https://www.geeksforgeeks.org/computer-networks/what-is-a-network-switch-and-how-does-it-work/)

[Difference between Router and Gateway](https://www.geeksforgeeks.org/computer-networks/difference-between-router-and-gateway/)

[Default Gateway in Networking](https://www.geeksforgeeks.org/computer-networks/default-gateway-in-networking/)

[Routing](https://www.geeksforgeeks.org/computer-networks/what-is-routing/)

[Routing Tables in Computer Networks](https://www.geeksforgeeks.org/computer-networks/routing-tables-in-computer-network/)

[Longest Prefix Matching in Routers](https://www.geeksforgeeks.org/computer-networks/longest-prefix-matching-in-routers/)

[Static and Dynamic Routing](https://www.geeksforgeeks.org/computer-networks/difference-between-static-and-dynamic-routing/)

#### Community References

The following README files were consulted for inspiration regarding structure and presentation:

- [42sp-cursus-netpractice by caroldaniel](https://github.com/caroldaniel/42sp-cursus-netpractice/blob/main/README.md)
- [NetPractice by lpaube](https://github.com/lpaube/NetPractice/blob/main/README.md)

### Use of AI

Google Gemini was used to clarify networking concepts and answer conceptual questions during the learning process.

ChatGPT was used to review the technical accuracy of the explanations, improve the organization of the README and assist with its writing.

All networking concepts were manually studied and understood before being included in this document.