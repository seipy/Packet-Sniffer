# Python 3 Network Packet Sniffer

[![Python Version](https://img.shields.io/badge/python-3.x-blue?style=for-the-badge&logo=python)](https://github.com/EONRaider/Packet-Sniffer/)
[![Open Source? Yes!](https://img.shields.io/badge/Open%20Source%3F-Yes!-green?style=for-the-badge&logo=appveyor)](https://github.com/EONRaider/Packet-Sniffer/)
[![License](https://img.shields.io/github/license/EONRaider/Packet-Sniffer?style=for-the-badge)](https://github.com/EONRaider/Packet-Sniffer/blob/master/LICENSE)

[![Reddit](https://img.shields.io/reddit/user-karma/combined/eonraider?style=flat-square&logo=reddit)](https://www.reddit.com/user/eonraider)
[![GitHub](https://img.shields.io/github/followers/eonraider?label=GitHub&logo=github&style=flat-square)](https://github.com/EONRaider)
[![Twitter](https://img.shields.io/twitter/follow/eon_raider?style=flat-square&logo=twitter)](https://twitter.com/intent/follow?screen_name=eon_raider)

A simple pure-Python network packet sniffer. Packets are disassembled
as they arrive at a given network interface controller and their information
is displayed on the screen.

This application maintains no dependencies on third-party modules and can be
run by any Python 3.x interpreter.

## Installation

### GNU / Linux

Simply clone this repository with `git clone` and execute the `packet_sniffer.py`
file as described in the following [Usage](#usage) section.

```sh
user@host:~/DIR$ git clone https://github.com/EONRaider/Packet-Sniffer.git
```

### Other Systems

This project is dependent on `PF_PACKET` - a stateful packet filter not
found on Windows or macOS X. For demonstration purposes, you can try out this
package in a Docker container. Although it will not have full access to
localhost on your machine, you can still sniff on the Docker subnet and at
least get the module running.

Use this command to build and run from the project directory:

```sh
docker build -t sniff . && docker run --network host sniff
```

Note that the entry command is simply `python packet_sniffer.py`, so feel
free to use the full functionality of the module by overriding the default
command. Remember that we tagged the container with the name "sniff"
before, so we can pass command-line arguments to the sniffer in the
following manner:

```sh
docker run --network host sniff [your command goes here]
echo "Now let's print help"
docker run --network host sniff python packet_sniffer.py --help
```

Usage of `--network host` is not supported on OS X or Windows
so this container won't be fully functional - but you will see packets
traveling within the docker subnet.

## Usage

```
packet_sniffer.py [-h] [-i INTERFACE] [-d]

A pure-Python network packet sniffer.

optional arguments:
  -h, --help            show this help message and exit
  -i INTERFACE, --interface INTERFACE
                        Interface from which packets will be captured (set to None to
                        capture from all available interfaces by default).
  -d, --displaydata     Output packet data during capture.
```

## Running the Application

- Execute the following command with administrative privileges to
  initiate the capture of packets on all available interfaces:

```sh
user@host:~$ sudo python3 packet_sniffer.py
```

- Sample output captured during execution:

```
[>] Packet #476 at 17:45:13:
    [+] MAC ......ae:45:39:30:8f:5a -> dc:d9:ae:71:c8:b9
    [+] IPv4 ..........192.168.1.65 -> 140.82.113.3    | PROTO: TCP TTL: 64
    [+] TCP ..................40820 -> 443             | Flags: 0x010 > ACK
[>] Packet #477 at 17:45:14:
    [+] MAC ......dc:d9:ae:71:c8:b9 -> ae:45:39:30:8f:5a
    [+] IPv4 ..........140.82.113.3 -> 192.168.1.65    | PROTO: TCP TTL: 49
    [+] TCP ....................443 -> 40820           | Flags: 0x010 > ACK
[>] Packet #478 at 17:45:18:
    [+] MAC ......dc:d9:ae:71:c8:b9 -> ae:45:39:30:8f:5a
    [+] ARP Who has  192.168.1.65 ? -> Tell 192.168.1.254
[>] Packet #479 at 17:45:18:
    [+] MAC ......ae:45:39:30:8f:5a -> dc:d9:ae:71:c8:b9
    [+] ARP ...........192.168.1.65 -> Is at ae:45:39:30:8f:5a
```

## Legal Disclaimer

The use of code contained in this repository, either in part or in its totality,
for engaging targets without prior mutual consent is illegal. **It is
the end user's responsibility to obey all applicable local, state,
and federal laws.**

Developers assume **no liability** and are not
responsible for misuses or damages caused by any code contained
in this repository in any event that, accidentally or otherwise, it comes to
be utilized by a threat agent or unauthorized entity as a means to compromise
the security, privacy, confidentiality, integrity, and|or availability of
systems and their associated resources by leveraging the exploitation of known
or unknown vulnerabilities present in said systems, including, but not limited
to the implementation of security controls, human- or electronically-enabled.

The use of this code is **only** endorsed by the developers in those
circumstances directly related to **educational environments** or
**authorized penetration testing engagements** whose declared purpose is that
of finding and mitigating vulnerabilities in systems, limiting their exposure
to compromises and exploits employed by malicious agents as defined in their
respective threat models.
