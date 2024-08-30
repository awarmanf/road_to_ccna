
# Spanning Tree

## Contents

  * [Introduction](#introduction)
  * [Spanning Tree Protocol Characteristics](#spanning-tree-protocol-characteristics)
    + [STP](#stp)
    + [PVST+](#pvst)
    + [RSTP](#rstp)
    + [Rapid PVST+](#rapid-pvst)
    + [MSTP](#mstp)
  * [Comparing Spanning Tree Protocols](#comparing-spanning-tree-protocols)
  * [BPDU](#bpdu)


## Introduction

Spanning tree is a very important protocol in traditional networks, and once again, 
its primary purpose is to stop loops in a switched environment and not necessarily 
to stop them as quickly as we would like.

In the past, slower convergence was fine, but that's a major problem in today's 
environments where we run voiceover IP or other protocols that require very quick 
convergence. The original standard spanning tree, or 802.1D spanning tree, has been 
superseded by newer versions such as rapid spanning tree and multiple spanning tree.

## Spanning Tree Protocol Characteristics

Source [STP](https://www.ciscopress.com/articles/article.asp?p=2832407&seqNum=5)

### STP
	
- IEEE 802.1D is the original standard.
- STP creates one spanning-tree instance for the entire bridged network, regardless of the number of VLANs.
- However, because there is only one root bridge, traffic for all VLANs flows over the same path, which can lead to suboptimal traffic flows.
- This version is slow to converge.
- The CPU and memory requirements are lower than for all other STP protocols.

### PVST+

- This is a Cisco enhancement of STP that provides a separate STP instance for each VLAN.
- Each instance supports PortFast, BPDU guard, BPDU filter, root guard, and loop guard.
- This design allows the spanning tree to be optimized for the traffic of each VLAN.
- However, CPU and memory requirements are high due to maintaining separate STP instances per VLAN.
- Convergence is per-VLAN and is slow, like 802.1D.

### RSTP

- 802.1w is an evolution of 802.1D that addresses many convergence issues.
- Like STP, it provides only a single instance of STP and therefore does not address suboptimal traffic flow issues.
- The CPU and memory requirements are less than for Rapid PVST+ but more than for 802.1D.

### Rapid PVST+

- This is a Cisco enhancement of RSTP.
- Rapid PVST+ uses PVST+ and provides a separate instance of 802.1w for each VLAN.
- Each instance supports PortFast, BPDU guard, BPDU filter, root guard, and loop guard.
- This version addresses the convergence issues and the suboptimal traffic flow issues.
- The CPU and memory requirements are the highest of all STP implementations.

### MSTP

- IEEE 802.1s is based on the Cisco Multiple Instance Spanning-Tree Protocol (MISTP) which is often simply referred to as Multiple Spanning Tree (MST).
- The Cisco implementation is often referred to as Multiple Spanning Tree (MST).
- MSTP maps multiple VLANs into the same spanning-tree instance.
- It supports up to 16 instances of RSTP.
- Each instance supports PortFast, BPDU guard, BPDU filter, root guard, and loop guard.
- The CPU and memory requirements are less than for Rapid PVST+ but more than for RSTP.

## Comparing Spanning Tree Protocols

Protocol | Standard | Resources Needed | Convergence | STP Tree Calculation
---------|----------|------------------|-------------|---------------------
STP | IEEE 802.1D | Low | Slow | All VLANs
PVST+ | Cisco | High | Slow | Per VLAN
RSTP | IEEE 802.1w | Medium | Fast | All VLANs
Rapid PVST+ | Cisco | High | Fast | Per VLAN
MSTP (MST) | IEEE 802.1s, Cisco | Medium or high | Fast | Per instance

## BPDU

Bridge protocol data units or BPDUs are sent out of all ports on switches by default every two seconds when running spanning tree.
So switches will learn about each other when they receive BPDUs from other switches on their ports.

As an example, in this topology, switch one will know that there's a loop because it's receiving a BPDU from switch two
on port two as well as port three. So BPDUs from a switch with the same bridge ID are received on multiple ports and thus switch one knows
that there's a loop between itself and switch two.

![Topology 2 switch](07.png)

In the same way, switch two knows that there's a loop because it receives BPDUs from switch one on both port one and port three.

In other words, it's receiving BPDUs from the same switch on multiple ports, hence there must be a loop.


