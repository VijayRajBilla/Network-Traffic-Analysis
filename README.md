# Network-Traffic-Analysis
Building a Network Packet Sniffer
## Network Traffic Analysis

This Python application is a simple packet sniffer designed to capture and decode Ethernet frames from a specified network interface. It leverages raw sockets to access the data link layer and utilizes dynamic protocol attachment for decoding various network protocols, including Ethernet, IPv4, IPv6, ARP, TCP, UDP, ICMPv4, and ICMPv6.

## Features

- **Decoding Multiple Protocols:** The packet sniffer dynamically attaches protocol decoders based on the protocols present in the captured frames. It supports decoding multiple protocols encapsulated within each other.

- **Observer Pattern:** The application follows the observer pattern, allowing multiple output modules to register for further processing of the decoded frames. This enables extensibility and the addition of new output modules.

- **Output to Screen:** An example output module, `OutputToScreen`, is provided, displaying decoded information to the console. It supports various protocols and displays relevant details such as Ethernet addresses, frame lengths, and protocol-specific information.

## Methodologies

## Raw Socket Access

The packet sniffer utilizes raw sockets provided by the `socket` module to access the data link layer directly. This allows the application to capture Ethernet frames without relying on higher-level protocols that might filter or modify the data.

## Dynamic Protocol Attachment

The decoding process is designed to be dynamic and extensible. The `_attach_protocols` method dynamically attaches protocol decoders based on the protocols present in the captured frames. This is achieved by iterating through a protocol queue and instantiating protocol decoder classes from the `netprotocols` module. The decoding process continues until the innermost protocol is reached.

## Observer Pattern

The observer pattern is employed to facilitate modular and extensible output processing. The `PacketSniffer` class acts as a subject, and output modules (observers) register themselves to receive updates on decoded frames. This allows for easy addition of new output modules without modifying the core sniffer logic.

# Results

## Output to Screen

The provided `OutputToScreen` module serves as a demonstration of the application's capabilities. It displays relevant information extracted from the decoded frames, including Ethernet addresses, frame length, timestamps, and protocol-specific details such as IP addresses, ports, and protocol types.

### Example Output

```
[>] Frame #1 at 10:30:45:
    [+] Ethernet 00:11:22:33:44:55 -> 66:77:88:99:aa:bb
        Interface: eth0
        Frame Length: 98
        Epoch Time: 1641605445.123456789

    [+] IPv4 192.168.1.2 -> 8.8.8.8
        DSCP: 0
        Total Length: 84
        ID: 12345
        Flags: 0
        TTL: 64
        Protocol: TCP
        Header Checksum: 0x1a2b

    [+] TCP 12345 -> 80
        Sequence Number: 987654
        ACK Number: 123456
        Flags: 0x18 > ACK, PSH
        Window Size: 65535
        Checksum: 0x3c4d
        Urgent Pointer: 0
```

This example output demonstrates the decoding of an Ethernet frame containing an IPv4 packet with a TCP payload. The displayed information includes Ethernet addresses, IPv4 addresses, TCP ports, sequence numbers, acknowledgment numbers, flags, window sizes, checksums, and more.

# Conclusion

The packet sniffer provides a flexible and extensible platform for capturing and decoding Ethernet frames. Its modular design allows for the easy addition of new protocols and output modules, making it a valuable tool for network analysis and troubleshooting. Developers can extend its functionality further by implementing additional protocols or custom output modules to suit specific requirements.
## Usage

### Prerequisites

- This application requires administrator privileges to run, as it involves raw socket access.
- Python 3.x is required.

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/VijayRajBilla/Network-Traffic-Analysis.git
   cd Network-Traffic-Analysis
   ```

2. Install dependencies:

   ```bash
   pip install -r required.txt
   ```

### Running the Packet Sniffer

Execute the following command to run the packet sniffer:

```bash
sudo python main.py -i <INTERFACE> -d
```

- Replace `<INTERFACE>` with the network interface from which Ethernet frames will be captured. If not specified, the sniffer monitors all available interfaces.

- The `-d` option is optional and, when provided, outputs packet data during capture.

### Exiting the Sniffer

To stop the packet capture, press `Ctrl-C`. The application will display a message indicating the capture is aborted.

## Extending the Functionality

- Developers can extend the functionality by implementing additional output modules. To do this, create a new class that inherits from the `Output` abstract base class and implement the `update` method.

- Register the new output module by creating an instance of it and passing it to the `PacketSniffer` as an observer.
