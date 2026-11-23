# Wireless LAN Security Assessment: Evil Twin & Man-in-the-Middle

A hands-on **WLAN vulnerability assessment**. It shows how attackers abuse untrusted Wi-Fi with an **Evil Twin rogue access point** (captive-portal credential harvesting) and a **Man-in-the-Middle (MITM)** attack (ARP spoofing and HTTP credential capture), and then proposes countermeasures.

> Wireless & Mobile Security coursework (individual). Every test was done in a **controlled lab against my own network and devices**, with authorisation.

---

## Hypothesis
Users who connect to a spoofed access point without verifying it are exposed to credential theft and traffic interception, even when the real network uses WPA2.

## Lab Setup
| Component | Role |
|---|---|
| VMware Workstation + **Kali Linux** | Attacker platform |
| **Atheros AR9271** USB adapter | Monitor mode and packet injection |
| **Airgeddon** | Evil Twin attack framework |
| **Bettercap** | MITM framework |
| Smartphone + laptop | Victim devices |

## Attack 1: Evil Twin
1. Put the adapter into **monitor mode**
2. **Reconnaissance**: scan nearby networks (BSSID, channel, encryption)
3. Select the authorised WPA2 target network
4. **Deauthentication** (aireplay-ng) to disconnect clients
5. **Capture and verify the WPA2 handshake** (PMKID also collectable)
6. Launch the rogue AP with a **captive portal** (DHCP, DNS and web server services)
7. The victim connects to the rogue AP and is shown a fake login page
8. **Credential validation**: a wrong password is rejected against the captured handshake, and the correct one is captured

## Attack 2: Man-in-the-Middle
1. Start Bettercap and enable **ARP spoofing**
2. **Network enumeration** (`net.show`) to find active hosts
3. The victim opens an HTTP login page
4. **Cleartext HTTP POST credentials captured** by Bettercap

## Countermeasures
- **WPA3 / 802.1X (WPA2-Enterprise)** with certificate validation
- **802.11w Protected Management Frames** against deauthentication attacks
- **Wireless IDS/IPS** and rogue-AP detection
- **HTTPS everywhere / HSTS**, and VPN on untrusted networks
- **Dynamic ARP Inspection** and DHCP snooping
- User awareness: verify networks and never enter Wi-Fi passwords into web portals

---

## Skills Demonstrated
802.11 security · WPA2 handshake capture · rogue AP and social-engineering attacks · ARP spoofing · traffic interception · defensive recommendations

## Tools
Kali Linux · Airgeddon · aircrack-ng suite · Bettercap · VMware Workstation · Atheros AR9271

## Author
**Sultan Mohammed Rabea** · [LinkedIn](https://www.linkedin.com/in/sultan-rabea/) · [GitHub](https://github.com/sultanrabea4)
