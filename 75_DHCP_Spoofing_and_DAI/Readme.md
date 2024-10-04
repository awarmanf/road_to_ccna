# DHCP Snooping

DHCP Snooping is a security feature that acts like a firewall between untrusted hosts and trusted DHCP servers.

Performs the following activities:

- Validates DHCP messages received from untrusted sources and filters out invalid messages.
- Rate-limits DHCP traffic from trusted and untrusted sources.
- Builds and maintains the DHCP snooping binding database, which contains information about untrusted hosts with leased IP addresses.
- Utilizes the DHCP snooping binding database to validate subsequent requests from untrusted hosts.

[![DHCP Snooping: Stop Kali DHCP Hacks and MITM](00-dhcp-snooping.jpg)](https://youtu.be/S6KI6VsvDuU)

Click the image to open the youtube video.

## DHCP Configuration

Configuration examples per network diagram

- Substitute VLAN 1 with your VLAN
- Substitute g0/0 and g0/1 with the interfaces you use

Enable DHCP snooping:

    conf t
    ip dhcp snooping
    ip dhcp snooping vlan 1
    no ip dhcp snooping information option
    exit
    show ip dhcp snooping

Specify trusted ports:

    conf t
    int G0/0
    ip dhcp snooping trust

Optional: Rate limit untrusted ports (packets per second)

    int G0/1
    ip dhcp snooping limit rate 10
    end

Optional: Auto-recover err-disabled ports after 30 seconds:

    conf t
    errdisable recovery cause dhcp-rate-limit
    errdisable recovery interval 30
    end

## Verification

Verify that it is working:

    show ip dhcp snooping
    debug ip dhcp snooping events
    debug ip dhcp snooping packets

## References

Go here for more:

- [Catalyst 6500 Release 12.2SX Software Configuration Guide](http://bit.ly/ciscodhcp)
- [Catalyst 4500 Series Switch Software Configuration Guide, 12.2(53)SG])http://bit.ly/dhcpsnoop)
- [David Bombal](http://www.davidbombal.com)


