# AD-Security-Assessment-Lab
Simulation of a controlled Active Directory Lab for adversary emulation and security testing.

## Lab infrastructure:

I decided to build this virtualized lab using **QEMU/KVM** simulating a small enterprise network. This network has the following infrastructure specification:


![](<./assets/Network_map.png>)


# What I will learn

![](<./assets/Possible_attacks.png>)

This are all the possible attacks that I can do in this lab. I think that all of this scenarios will allow me to understand the AD service from an starting point.

### Key objectives:

- **Network Poisoning:** Exploiting the protocols LLMNR/NBT-NS and IPv6.
- **Credential Harvesting:** Using tools like Responder, Mimikatz and Impacket
- **Lateral movement:** With the techniques SMB Relay and Pass-the-Hash.
- **Privilege scalation:** Identifying misconfigurations in GPOs and Service Principal Names (Kerberoasting)


### ⚠️ Legal Disclaimer:
This repository is for educational and security research purposes only. All attacks were performed in a strictly controlled, private laboratory environment. Unauthorized access to computer systems is
illegal.
