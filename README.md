# Prolog Assignment - Firewall Rules encoding

## Problem Statement

- Firewall rules are encoded in Prolog as facts and rules:
- Each rule may start with accept (allow the incoming packet), reject (send reject information to sender), or drop (silently) followed by a clause. See documentation [here](https://www.ibm.com/support/knowledgecenter/en/SSETBF_3.1.1/com.ibm.siteprotector.doc/references/pam_filter_sets.html)
- Write a Prolog program to apply encoded rules on any incoming packet.
- Note that multiple rules may apply.
- 3-person teams are to handle everything. 2-person teams need not handle IPV6 and ICMPv6 clauses and conditions

## How to Run?

You need a Prolog Environment installed ([SWI-Prolog](http://www.swi-prolog.org/) is preferred) to run this program.

## User Interface

- The top level procedure is printStatus(`<packetname>`)
- The procedure prints Packet Accepted, Packet Rejected or Packet Dropped. If there is a conflict in the status of the packet according to the rules, priority is given to reject, then drop, and then accept.
- Example:

```prolog
    ?- printStatus('pack1').
    Packet Accepted
```

## Rule base

- The rule base contains rules as required. Each rule starts with an accept,reject or drop predicate. Each is a unary predicate, which takes a string argument.
- The default behaviour of the program is to accept; which means that if the packet is unmatched to any of the rules, it will be accepted.
- Example:

```prolog
    accept(‘ip src addr 172.24.6.31’).
    reject(‘adapter C-F’).
    drop(‘ether vid 3-199 proto 0x0800,0x86dd’).
```

## Packet Input Format

- Each packet is encoded in the database within the predicate packet(<'packet_name',attribute_list>).
  - `packet_name` is any string.
  - `attribute_list` is a list containing 16 attributes of the packet, all enclosed in quotes.
    - Not all of these attributes will be applicable for a given packet.

```prolog
['Src_ip','Dst_ip','Adapter_num','Protocol_type', 'Icmpv6_type','Icmpv6_Msgcode','Vlan_Id', 'TCPSrc','TCPDst','UDPSrc','UDPDst','IPV6Src','IPV6Dst','ICMPType','ICMPCode','protocolId']
```

- The terms are described below:
  - `Src_ip`: The ipv4 address of the source.
  - `Dst_ip`: The ipv4 address of the destination.
  - `Adapter_num`: Adapter number, an upper case character between A and H. Note: Specified in double quotes rather than single.
  - `Protocol_type`: The protocol type specified in ip datagram clause (tcp/udp) Note: Specified in double quotes rather than single.
  - `Icmpv6_type`: Protocol type specified in icmpv6 conditions(integer)
  - `Icmpv6_Msgcode`: message code specified in icmp conditions(integer).
  - `Vlan_Id`: Virtual LAN Id (Integer, specified in the ethernet clause)
  - `TCPSrc`:TCP port number of source between 0 and 65535.
  - `TCPDst`:TCP port number of destination between 0 and 65535.
  - `UDPSrc`:UDP port number of source between 0 and 65535.
  - `UDPDst`:UDP port number of destination between 0 and 65535.
  - `IPV6Dst`: ipv6 address of source
  - `IPV6Dst`: ipv6 address of destination
  - `ICMPType`: Protocol type in ipv6
  - `ICMPCode`: Message code in ipv6
  - `protocol-id`: The protocol id specified in the `ether proto <protocol_id>` clause

The parameters for ipv4 and ipv6 are mutually exclusive; so are the parameters for tcp and udp. For the values not to be given, an asterisk '*' should be used.

Examples can be found in FactsDatabase.pl

## Group Members

- [Harpinder Jot Singh](https://github.com/HarpinderJotSingh)
- [Vishal Mittal](https://github.com/vismit2000)
- [Yash Vijay](https://github.com/yashvijay018)
