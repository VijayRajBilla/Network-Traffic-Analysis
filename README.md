# Network-Traffic-Analysis
Building a Network Packet Sniffer
# Network Traffic Analysis

This Python application is a simple packet sniffer designed to capture and decode Ethernet frames from a specified network interface. It leverages raw sockets to access the data link layer and utilizes dynamic protocol attachment for decoding various network protocols, including Ethernet, IPv4, IPv6, ARP, TCP, UDP, ICMPv4, and ICMPv6.

## Features

- **Decoding Multiple Protocols:** The packet sniffer dynamically attaches protocol decoders based on the protocols present in the captured frames. It supports decoding multiple protocols encapsulated within each other.

- **Observer Pattern:** The application follows the observer pattern, allowing multiple output modules to register for further processing of the decoded frames. This enables extensibility and the addition of new output modules.

- **Output to Screen:** An example output module, `OutputToScreen`, is provided, displaying decoded information to the console. It supports various protocols and displays relevant details such as Ethernet addresses, frame lengths, and protocol-specific information.

## Usage

### Prerequisites

- This application requires administrator privileges to run, as it involves raw socket access.
- Python 3.x is required.

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/your_username/packet-sniffer.git
   cd packet-sniffer
   ```

2. Install dependencies:

   ```bash
   pip install -r requirements.txt
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
