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

