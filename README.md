#  Attacking Active Directory: Initial Attack Vectors

This repository documents techniques and tools used in the **initial stages** of attacking Active Directory (AD) environments. It includes practical demonstrations and defenses for common attack vectors such as LLMNR poisoning and SMB relaying.

---

##  Table of Contents
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
- Common tools: `Responder`,.

---

## 3. Capturing NTLMv2 Hashes with Responder

Responder can capture NTLMv2 hashes via LLMNR/NBT-NS spoofing:

```bash
sudo responder -I eth0
`````

-**-m 5600:** Specifies NTLMv2 hash mode
-**hashes.txt:** File containing the captured hashes
-**rockyou.txt:** Wordlist used for the attack (can be replaced with custom wordlists)
-**--force:** Optional flag to override warnings

---

## 4. LLMNR Poisoning Defense
- To protect your environment from **LLMNR/NBT-NS** spoofing attacks:


