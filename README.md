# 🛡️ Attacking Active Directory: Initial Attack Vectors

This repository documents techniques and tools used in the **initial stages** of attacking Active Directory (AD) environments. It includes practical demonstrations and defenses for common attack vectors such as LLMNR poisoning and SMB relaying.

---

## 📌 Table of Contents
1. [Introduction](#1-introduction)  
2. [LLMNR Poisoning Overview](#2-llmnr-poisoning-overview)  
3. [Capturing NTLMv2 Hashes with Responder](#3-capturing-ntlmv2-hashes-with-responder)  
4. [Password Cracking with Hashcat](#4-password-cracking-with-hashcat)  
5. [LLMNR Poisoning Defense](#5-llmnr-poisoning-defense)  
6. [SMB Relay Attacks Overview](#6-smb-relay-attacks-overview)  

---

## 1. Introduction

Active Directory (AD) is a key target in most enterprise networks. Initial access and privilege escalation often begin with misconfigurations in network services. This guide covers some of the most widely used attack vectors for gaining a foothold in AD environments.

---

## 2. LLMNR Poisoning Overview

- **LLMNR** (Link-Local Multicast Name Resolution) is a fallback name resolution protocol.
- Often enabled by default in Windows networks.
- Vulnerable to spoofing and man-in-the-middle attacks.
- Common tools: `Responder`, `MITMf`.

---

## 3. Capturing NTLMv2 Hashes with Responder

Responder can capture NTLMv2 hashes via LLMNR/NBT-NS spoofing:

```bash
sudo responder -I eth0

It listens for broadcast name resolution requests.

Spoofs responses to trick the victim into authenticating to the attacker.

NTLMv2 hashes are captured and stored for cracking.

4. Password Cracking with Hashcat
Use Hashcat to crack captured NTLMv2 hashes:

hashcat -m 5600 hashes.txt rockyou.txt --force
-m 5600: NTLMv2 format

Use rockyou.txt or custom wordlists.

Strong GPU = faster cracking.

5. LLMNR Poisoning Defense
Disable LLMNR and NBT-NS via Group Policy:


Computer Configuration > Admin Templates > Network > DNS Client
Enforce strong password policies.

Use SMB signing to prevent relay attacks.

Monitor for Responder/rogue traffic using tools like Zeek or endpoint EDRs.

6. SMB Relay Attacks Overview
Instead of capturing hashes, SMB Relay attacks use those hashes in real-time to authenticate against another system.

Tool: ntlmrelayx.py from Impacket

Commonly used to pivot and escalate privileges.


sudo ntlmrelayx.py -tf targets.txt -smb2support
Requires SMB signing to be disabled.

Can lead to shell access or dumping of sensitive files.

Disclaimer
This repository is for educational and ethical hacking purposes only. Never use these techniques on systems without explicit permission.


