ill pry open malwares or expose them like dotstealer backdoored in the assembly


# DotStealer (Gurcu / Whitesnake) - Malware Analysis

> 🛑 **This project does NOT contain malware. This repository is intended for educational and research purposes only.**  
> No binaries or functioning payloads are included. Please do not use this information for malicious purposes.

---

## 🧾 Summary

This is a technical analysis of **DotStealer**, also known in some circles as **Gurcu** or **Whitesnake**. It is a commodity .NET-based stealer sold for around **$30** on various forums. During static analysis, it was found to be **backdoored**, quietly exfiltrating data to a hardcoded Telegram bot, regardless of what the buyer configures in the builder.

---

## 🔍 Key Findings

- Written in **C# (.NET Framework)**
- Decompiled using **dnSpy**
- Builder interface is user-friendly but implants a **hardcoded Telegram token and chat ID**
- Obfuscation is minimal: C2 info is **Base64-encoded and then ROT13-encoded**
- Designed to be **single-executable** (using techniques like Costura or ILMerge)
- No admin rights required for most functionality

---

## 🔐 Backdoor Behavior

- The compiled payload **always contains a hardcoded Telegram bot token and chat ID** embedded in the source.
- These credentials do **not change** when the builder is reconfigured.
- Any logs stolen by the payload are **silently sent to the attacker's own Telegram channel** in addition to the buyer's configured destination.

btw dead token and chatid

https://tria.ge/250508-2b5w5aypz5/behavioral2


2nd malware

🎬 Introduction
In early 2025, a previously underground malware family known as NeptuneRAT resurfaced, drawing the attention of independent researchers and threat analysts. Initially marketed as a modern Remote Access Trojan (RAT) for "educational purposes," NeptuneRAT quickly gained notoriety for being backdoored, feature-rich, and actively destructive.

This documentary-style brief exposes the inner workings of NeptuneRAT — from its rootkit loader and embedded dual-RAT payloads, to its hidden “fun panel” capable of wiping machines with a single click.

🧬 Malware Architecture
📁 Stub (Initial Loader)
The infection begins with a stub, often disguised as a cracked tool or installer. Upon execution, it loads a concealed rootkit with elevated privileges.

🦠 Rootkit
The rootkit is not a simple packer. It serves as the primary payload container, embedding two notorious RATs:

xWorm: A modular, modern Trojan with capabilities like DDoS, clipboard hijacking, persistence, and more.

njRAT: A legacy but powerful surveillance tool with webcam, microphone, and remote shell access.

The rootkit provides stealth, persistence, and execution control of both embedded malware strains.

🌐 C2 Infrastructure
🕸 Primary Domain
abolhb[.]com — the known command-and-control (C2) server

Likely registered via bulletproof hosting

Suspected to serve malware updates, commands, and plugin payloads

📡 Network Behavior
HTTP(S) and TCP-based command channels

Periodic beaconing

DNS tunneling likely involved

🎮 Command Panel – “Fun Panel”
What sets NeptuneRAT apart is its administrative control panel, which includes a section referred to in code and by users as the “fun panel.”

🚨 Destructive Capabilities Include:
System file wipers

Registry corruption

Forced BSOD

Fake Windows Updates (crash loopers)

Payload delivery that bricks machines

This is not just spyware — it's a fully weaponized RAT with kill-switch level controls.

📜 Version History
🔹 Version 1
deleted off github

Used by script kiddies and low-level actors

Lacked stealth and had simple persistence

🔹 Version 2
Embedded xWorm and njRAT
deleted off github 

Integrated destructive panel

Deleted from circulation after reports of backdooring — the creator had inserted their own C2 & spyware to spy on users of the tool

🕵️‍♂️ Research Notes
The stub loads the rootkit in memory, avoiding traditional AV

Anti-debugging and sandbox evasion are implemented

The rootkit appears to hook system calls for file hiding and process cloaking

File hashes, mutex names, and C2 behaviors align with known xWorm/njRAT samples

🔐 Indicators of Compromise (IOCs)
Type	Value
C2 Domain	abolhb[.]com
Embedded Tools	xWorm, njRAT
Behavior	Keylogging, file theft, wiper
Mutex Example	neptune_mutex_01 (sample)
Hashes	(MD5

39fd5e31eb34e8b98a89c78fd76354cf

SHA1

eac5246b5bef6f8a7d0dab40bf7b1a2a858e6acf

SHA256

912c932d1793e540542a27eff9968e298dc2fbbc8a3ece3765471c6d217f1ff4)

🧑‍💻 Attribution & Risk
While attribution is unclear, the use of dual RATs and an embedded backdoor strongly suggests:

A single operator or small group distributing this for both control and espionage

A false flag of "educational" usage masking real-world cybercrime

Risk Rating: 🔴 Severe – due to rootkit-level access, destructive payloads, and open-source distribution among threat actors.

sometimes a bootkit idk why

triage link: https://tria.ge/250404-qwpj4axya1
