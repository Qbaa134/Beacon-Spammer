![Projekt bez nazwy](https://github.com/user-attachments/assets/c55a62b6-598a-4503-94cc-8d73c1f7a948)
# 📡 Beacon Spammer Project 🚀

Hi! 👋 Welcome to the **Beacon Spammer** project, which allows you to generate fake Wi-Fi networks (SSIDs) using an ESP8266 microcontroller. This tool can be useful in various scenarios such as testing Wi-Fi network security 🔐, studying wireless device behavior 🧑‍💻, or simply experimenting with technology 💡.

# The latest version of the script also includes a Deauther!

> [!WARNING]
> This tool is intended for educational purposes and testing your own networks. Do not use it illegally on other people's networks.

# **NEW!**
## **You can now upload the script faster [from the project's official website](https://qbaa134.github.io/Beacon-Spammer).**

## 🎯 Project Goal

The goal of this project is to create a tool that emulates Wi-Fi networks by regularly sending beacon packets with fake SSIDs. Each beacon packet simulates a real Wi-Fi network, making nearby devices detect a "new" network. 🌍

You can configure an SSID prefix that will be added to each sent network. This allows you to easily generate a large number of different SSIDs that will be visible on other devices within range. 📱💻
### In the future, there will be the possibility to use an `OLED` screen, buttons, and the implementation of other hacking features!

## 📦 Requirements

![image](https://github.com/user-attachments/assets/6d378cec-3d35-4e42-a325-15104f413880)
To run the script, you will need:
- ESP8266 microcontroller (e.g., NodeMCU, Wemos D1 Mini)
- **Arduino IDE environment** with the appropriate ESP8266 setup or [the project website](https://qbaa134.github.io/Beacon-Spammer)
- USB cable to connect the microcontroller to your computer
- (Optional) Additional Arduino libraries

### Optional parts:
- LiPo battery (preferably 1000mAh)
- Tp4056 module
- RGB LED K851264
- 10uF capacitor
- Wires and cables
- Mini SPDT switch
- Mini Step Up converter 3.7V -> 5V
- (Optional Schottky diode)

## 🔌 Wiring
![Wiring Diagram](https://github.com/user-attachments/assets/6b8b0966-31f0-4986-8b04-8d0c86dcdeed)

| **Source**        | **Destination**  |
|-------------------|------------------|
| LiPo +            | Tp4056 B+        |
| LiPo -            | Tp4056 B-        |
| Tp4056 OUT +      | Switch           |
| Tp4056 OUT -      | Step Up -        |
| Switch            | Step Up +        |
| Step Up +         | 10uF             |
| Step Up -         | 10uF             |
| Step Up OUT +     | 5V               |
| Step Up OUT -     | G                |
| RGB GND           | G                |
| RGB R             | D5               |
| RGB B             | D7               |
| RGB G             | D6               |

LED colors:
- Red: No activity
- Blue: Client connected to AP
- Green: Packet transmission in progress / Attack Started

## Installation
### Arduino IDE
1. **Install Arduino IDE**: If you don't have it yet, download and install Arduino IDE from the [official website](https://www.arduino.cc/en/software).
   
2. **Configure ESP8266 in Arduino IDE**:
   - Open Arduino IDE.
   - Go to `File` → `Preferences` and add the following URL in "Additional Boards Manager URLs": `http://arduino.esp8266.com/stable/package_esp8266com_index.json`.
   - Go to `Tools` → `Board` → `Boards Manager`, search for `ESP8266`, and install the appropriate version.
   
3. **Upload the code to ESP8266**: Copy the project code into a new sketch in Arduino IDE and upload it to your ESP8266 microcontroller.

4. **Monitor data in the serial monitor**: After uploading the program, you can monitor the SSID packet generation process using the `Serial Monitor` in Arduino IDE.

### Bin Files
1. In your browser, go to the [project website](https://qbaa134.github.io/Beacon-Spammer) and select the software version.
   - Classic version with network names hardcoded in the script.
   - Version with a web interface where you enter network names.
2. Click `Connect`, proceed, and upload the file.

## Web Interface Version
1. After uploading the software, connect to the Wi-Fi network `beacon` with the password `password`.
2. In your browser, enter the ESP8266's IP address: `192.168.4.1` or [click this link](http://192.168.4.1/).
3. Enter 100 SSIDs and click the `Green Button`.
4. Open the [serial monitor](https://qbaa134.github.io/esp-tool/) and connect to the ESP8266.
![image](https://github.com/user-attachments/assets/c70ba991-65eb-4a4b-bf80-91f123b81345)

- `SSID_name`
- `SSID_name`
- `SSID_name`  
- `SSID_name`
- `etc.`

## Entering the Same SSID
To make the networks appear identical, add a special character at the end of the SSID.
- `networkx`  
- `networkx` (contains a hidden character after the name)
- `networkx` (two hidden characters)
- `networkx` (three hidden characters)
- `networkx` (four hidden characters)
- `etc.`

1. Copy the Zero-Width Space character:

`  `← zero-width space here (U+200B)

It looks like an "empty line," but the character is there. Paste it at the end of the SSID as many times as you want.

2. You can also type it using the key combination:

Alt + 8203 (on the numeric keypad)

These two methods will add U+200B at the cursor position.

## RGB Version
The RGB version is the same as the web interface version, but we connect an LED to the ESP, which lights up in different colors depending on the function being performed.

# ⚠️ESP8266 Deauther⚠️

## What is a Deauther?

A Deauther is specialized software that runs on an ESP8266 (or ESP32) microcontroller and allows you to perform Wi-Fi network tests by sending deauthentication and disassociation packets. The main purpose is education and testing wireless network security. This project is popular among ethical hackers and pentesters.

# Deauther Installation
1. In your browser, go to the [project website](https://qbaa134.github.io/Beacon-Spammer) and select the option with "Deauther" in the name.
   - WiFi Deauther (ESP8266).
2. Click `Connect`, proceed, and upload the file.
3. After uploading, the Deauther disconnects devices from all available networks.
### Warning! Use this script only on your own networks!

## How Does the Deauther Work?

The Deauther uses the ESP8266's ability to monitor and send Wi-Fi frames. Its operation is based on vulnerabilities in the 802.11 standard, which allows sending unencrypted control frames—including deauth and disassoc frames.

- **Deauthentication** — the packet informs the client that it has been unauthorized from the network. The client disconnects from the router.
- **Disassociation** — the packet tells the client that the connection with the access point has been terminated. The client does not fully disconnect but must renegotiate the connection.

### Legality and Warning

The Deauther is an educational tool. Using it without the network owner's consent is illegal and may lead to legal consequences. The goal of this project is to raise awareness about Wi-Fi security.

Ready for further modifications, e.g., a configuration section?

## ⚙️ How Does Beacon Spammer Work?

The project is based on using the ESP8266's capabilities to emulate Wi-Fi networks by sending specially formatted beacon packets. These packets contain SSID (network name) information that will be visible to nearby devices.
## All information below refers to the `.ino` file.
### Beacon Packet Structure

Beacon packets contain various information, including:

- **Device MAC address**: A unique hardware identifier used by Wi-Fi networks.
- **SSID**: The Wi-Fi network name displayed to nearby devices.
- **WPA/WPA2 version**: Specifies the type of security used in the network (optional).

Each of these elements can be modified, providing great flexibility in manipulating what devices see in their list of available networks.

### Generating SSIDs

In this project, SSIDs are generated dynamically, and their names start with a specific prefix. For example, if you set the prefix to `MyFakeSSID_`, the generated SSIDs might look like this:

- `MyFakeSSID_1`
- `MyFakeSSID_2`
- `MyFakeSSID_3`
- etc.
<img src="https://github.com/user-attachments/assets/221b3a9a-a3d4-42a1-ae6d-21971daa90ac" alt="Image description" width="400"/>

This makes it easy to create many networks with different names, which is useful for security testing.

## 🛠️ Configuration

### Changing the SSID Prefix

To change the SSID prefix (i.e., the name of generated networks), simply edit/add the variable in the code:

```cpp
"yournetwork\n";
```

You can replace `"yournetwork"` with any string that will be the beginning of the network names.

### WPA2

The project includes the ability to enable/disable WPA2 mode. If you want your networks to be "secured" with WPA2, set the `wpa2` variable to `true`:

```cpp
const bool wpa2 = true;  // WPA2 mode
```

If you want the networks to be "open" (unencrypted), set it to `false`.

### MAC Address Randomization

MAC addresses are randomly generated using the `randomMac()` function, allowing the emulation of different devices. The first byte of the MAC address is set to `0x02`, meaning it is locally administered (intended for devices that generate random MAC addresses).

```cpp
void randomMac() {
  macAddr[0] = 0x02; // Unicast, locally administered
  for (int i = 1; i < 6; i++) {
     macAddr[i] = random(256);
  }
}
```

## 📊 Monitoring

During operation, you can track which SSIDs have been generated and the status of packet transmission on the `Serial Monitor`. This is especially helpful if you want to debug your code or check the performance of SSID generation.

## 🧰 Usage Examples

### Testing Wi-Fi Networks

You can use this project to test how different devices react to multiple available Wi-Fi networks. This will help you understand how operating systems (e.g., Android, Windows) detect and sort networks, and whether they can recognize fake SSIDs.

## 📦 Enclosure
If you have a Wemos D1 mini, you can print a dedicated enclosure using the **.3mf** file. This will better protect your device and give it a polished look.
![image](https://github.com/user-attachments/assets/a028a3a8-ed1c-46cb-9f28-6c569c86478f)

## 🚀 Future Developments

- **WPA3 Support** - Implementing beacon generation with support for the latest security standard  
- **Stealth Mode** - Random time intervals between packets to avoid detection  
- **Dynamic Channel Switching** - Automatic scanning and selection of optimal Wi-Fi channels   
- **Geofencing** - Auto-disabling transmission based on GPS location  
- **Advanced SSID Spoofing** - Generating realistic SSID names based on the environment  
- **Real-Time Statistics** - Data visualization in the form of charts on the web interface  
- **Enterprise WiFi Support** - Emulating corporate networks with 802.1X authentication  
- **Energy Saving Mode** - Optimizing power consumption for battery operation  
- **Multi-AP Synchronization** - Coordinating multiple devices for complex scenarios  
- **AI-Powered Patterns** - Generating network traffic using ML models  
- **Captive Portal Integration** - Creating interactive captive portals  
- **Bluetooth Low Energy Spoofing** - Extending with ESP32 for BLE device emulation  
- **OpenWRT Support** - Porting the solution to routers with custom firmware  
- **RF Shielding Analytics** - Monitoring signal masking effectiveness  
- **Cross-Platform Client** - Dedicated mobile app for device management  

## 🌟 Summary

**Beacon Spammer** is a great tool for experimenting with Wi-Fi technology, testing network security, and playing with microcontrollers. Thanks to its simplicity and configuration flexibility, you can adapt the project to your needs and implement interesting wireless network projects.

If you have any questions or suggestions about the project, feel free to share them! 🚀
