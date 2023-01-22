# `Air-Shark` - _WireShark Filters, Colors & Profile_
_by Fz3r0 (Former CWNA/CCNA)_

- **_"When wireless is perfectly applied the whole earth will be converted into a huge brain, which in fact it is, all things being particles of a real and rhythmic whole.  We shall be able to communicate with one another instantly, irrespective of distance... "_** <br> 
_Nikola Tesla (scientist, inventor) – Colliers Illustrated Weekly (1926)_<br>  

````
#########################################################################################
#                                      ,-                                               # 
#                                    ,'::|                                              # 
#                                   /::::|                                              #
#                                 ,'::::o\                                      _..     #
#              ____........-------,..::?88b                                  ,-' /      #
#      _.--""""./. . .      .   .  .  .  ""`-._                           ,-' .;'       #
#     <. - :::::o......  ...   . . .. . .  .  .""--._         .        ,-'. .;'         #
#      `-._  ` `":`:`:`::||||:::::::::::::::::.:. .  ""--._ ,'|     ,-'.  .;'           #
#          """_=--\      //'F0... ````:`:`::::::::::.:.:.:. .`-`._-'.   .;'             #
#              ""--.__     ((       \               ` ``:`:``:::: .   .;'               #
#                     "\""--.:-.     `.                             .:/                 #
#                       \. /    `-._   `.""-----.,-..::(--"".\""`.  `:\                 #
#                        `"         `-._ \          `-:\          `. `:\                #
#                                        ""            "            `-._)               #
#                     _     _         ____   _                   _                      #
#                    / \   (_) _ __  / ___| | |__    __ _  _ __ | | __                  #
#                   / _ \  | || '__| \___ \ | '_ \  / _` || '__|| |/ /                  #
#                  / ___ \ | || |     ___) || | | || (_| || |   |   <                   #
#                 /_/   \_\|_||_|    |____/ |_| |_| \__,_||_|   |_|\_\                  #
#                                                                                       #
#              802.11 Wireless (WiFi) Wireshark Filters, Colors & Profile               # 
#                                                                                       #
#                          [+] Author:..........Fz3r0                                   #
#                          [+] Github:..........github.com/Fz3r0                        #
#                          [+] Twitter:.........@Fz3r0_OPs                              #
#                          [+] Youtube:.........@Fz3r0_OPs                              #
#                                                                                       #
#########################################################################################
````

## Cheatsheets

### 802.11 Wireless `AirShark`:

- https://semfionetworks.com/wp-content/uploads/2021/04/wireshark_802.11_filters_-_reference_sheet.pdf
- https://wiki.wireshark.org/Wi-Fi
    - https://www.wireshark.org/docs/dfref/w/wlan.html
    - https://www.wireshark.org/docs/dfref/w/wlan_mgt.html
    - https://www.wireshark.org/docs/dfref/w/wlan_aggregate.html

### Decrypt 802.11 Wireless `AirShark`:

- https://wiki.wireshark.org/HowToDecrypt802.11    


## Addresses Used in 802.11 Communications

- Up to **4** different `MAC addresses` can be used in an `IEEE 802.11 frame`.

    - `Transmitter` & `Receiver` MAC addresses refer to the communication link between devices:

        - In a typical wireless communication, a `laptop` (`transmitter` = `TA`) may send a frame to a `Access Point` (`receiver` = `RA`) requesting access to the internet. 

    - `Source` & `Destination` MAC addresses refer to the origin and ultimate destination of the frame, respectively, regardless of the number of intermediate devices the frame passes through before reaching its final destination.

        - The `laptop` (`transmitter` = `TA`) is also the source of the frame that is requesting access to the internet (`source` = `SA`).
            - So, the laptop's MAC address would be the Source MAC address (SA) too: laptop-A (`transmitter = TA` & `source = SA`)

        - The `Destination` of the frame is the `Server` or `Website` the user wants to access. 
            - So, the server's MAC address in a far datacenter would be the `Destination MAC address (DA)`.

- `TA` = `laptop`
- `SA` = `laptop`
- `RA` = `Access Point (AP)`
- `DA` = `Web Server / URL / etc`

|           **Name**             | **Syntax** |                      **Description**                        |          **Wireshark Filter**        |
|:------------------------------:|:----------:|:-----------------------------------------------------------:|:------------------------------------:|
| **`CLIENT`**_(any WiFi client)_| `client`   | The MAC of any client in the whole WLAN (_`TA/RA/SA/DA`_)   | `wlan.addr == "client_MAC_Address" ` |
| **Transmitter MAC address**    | `TA`       | The MAC address of the device `transmitting` the frame.     | `wlan.ta == "TA_MAC_Address"`        |
| **Receiver MAC address**       | `RA`       | The MAC address of the device `receiving` the frame.        | `wlan.ra == "RA_MAC_Address"`        |
| **Source MAC address**         | `SA`       | The MAC address of the device `originating` the frame.      | `wlan.sa == "SA_MAC_Address"`        |
| **Destination MAC address**    | `DA`       | The MAC address of the device the frame is being `sent to`. | `wlan.da == "DA_MAC_Address"`        |

- You can filter for IPv4 Addresses too. 
- This filters are the same as other Wireshark profiles (ex. LAN/ETH-I filters)

|           **Name**          |  **Syntax**  |                      **Description**                     |        **Wireshark Filter**      |
|:---------------------------:|:------------:|:--------------------------------------------------------:|:--------------------------------:|
| **CLIENT(any WiFi client)** | `client`     | The IP of any client in the whole WLAN                   | `ip.addr == "client_IP_Address"` |
| **Source IP address**       | `SRC`        | The IP address of the device sending the frame.          | `ip.src == "TA_IP_Address"`      |
| **Destination IP address**  | `DST`        | The IP address of the device receiving the frame.        | `ip.dst == "RA_IP_Address"`      |


## **Types** of `Networks` Used in `802.11 / WiFi`

- A wireless network is made up of several components including:

    - `BSS` - A group of wireless devices that communicate with each other. "The whole WLAN"
    - `BSSID` - The specific MAC Address of the AP that a wireless frame is associated with.
    - `SSID` - Name of a wireless network, usually in plaintext. 
    - `ESS` - A Network that connects multiple & different BSSs together.
    - `IBSS` - A type of BSS that allows wireless devices to connect to each other without the need of an access point.
    - `DS` - Aystem that distributes data across a wireless network.
    - `Mesh network` - A type of wireless network where each device acts as a relay.
    - `WDS` - A system that allows wireless devices to connect without a wired connection.

- _**Note:** It's also worth noting that the BSSID is not necessarily the same as the MAC address of the wireless NIC of the AP. The BSSID can be set manually to any unique value by the administrator of the wireless network._

    - **IMPORTANT:** Not all of the components mentioned are mandatory for a wifi network to function. 
    - **The `WiFi Core Components` that are required for a wifi network to function include `BSS`, `BSSID` & `SSID`.**

|              **Name**                    |                                         **Description**                                                          |           **Wireshark Filter**         |
|:----------------------------------------:|:----------------------------------------------------------------------------------------------------------------:|:--------------------------------------:|
| **BSSID**                                | Identify the specific AP that a wireless frame is associated with. Also known as the MAC Address of the AP       | `wlan.bssid == "AP_radio_MAC_address"` |
| **SSID**                                 | Identify the specific network that a wireless frame is associated with in plain text string (ex. Infinitum_23)   | `wlan_mgt.ssid == "your_SSID"`         |
| **BSS: Infrastructure**                  | Identify Infraestructure Network that a wireless frame is associated with.                                       | `wlan_mgt.bss_type == 0`               |
| **BSS: Independent**                     | Identify Independent Network that a wireless frame is associated with.                                           | `wlan_mgt.bss_type == 1`               |
| **BSS: Centralized**                     | Identify Centralized Network that a wireless frame is associated with.                                           | `wlan_mgt.bss_type == 2`               |
| **ESS: Extended Service Set**            | Identify a group of interconnected BSSs that forms a single logical wireless LAN (WLAN) with a single SSID.      | `wlan_mgt.ssid == "your_SSID"`         |
| **IBSS: Independent Basic Service Set**  | Identify a BSS that does not have an AP and is formed by a group of devices.                                     | `wlan_mgt.bss_type == 1`               |
| **DS: Distribution System**              | Identify a system of wireless APs that interconnects multiple BSSs and provides roaming capabilities .           | `wlan_mgt.ds.current_channel`          |
| **Mesh Network**                         | Identify a type of wireless network in which the devices (nodes) communicate with each other to form a network.  | `wlan_mgt.mesh.config.active`          |
| **WDS: Wireless Distribution System**    | Identify a system that enables the wireless interconnection of access points in an IEEE 802.11 network.          | `wlan_mgt.wds.address`                 |


## Management Frames

- 802.11 `Management Frames` = `type = 0`
- Used to manage and control wireless networks. 
- Used by stations (STA) to join and leave a BSS 
- Typically sent at a lower data rate than regular data frames, and they are not acknowledged by the receiving device. 
- This allows them to be transmitted quickly and efficiently, without adding to network congestion. 
- These frames are used for various purposes such as:

    - `Association` & `Disassociation` - To connect and disconnect devices from a wireless network.
    - `Authentication` & `Deauthentication` - To verify the identity of devices attempting to connect to a wireless network.
    - `Beaconing` - To advertise the presence of a wireless network and provide information about its capabilities.
    - `Power management` - To control the power usage of wireless devices.
    - `Quality of Service (QoS)` - To prioritize different types of traffic on a wireless network.

- There is a total of **12** `802.11 Management Frames`:

|      **802.11 Frame**       | **Subtype** |                                     **Description**                                          |     **Wireshark Filter**     |     
|-----------------------------|:-----------:|:---------------------------------------------------------------------------------------------|------------------------------|
| **`ALL MANAGEMENT FRAMES`** | _N/A_       |                                                                                              | `wlan.fc.type == 0`          | 
| **Association Requests**    | `0x0`       |  Sent by a client to request association with an access point.                               | `wlan.fc.type_subtype == 0`  |
| **Association Responses**   | `0x1`       |  Sent by an access point in response to an association request.                              | `wlan.fc.type_subtype == 1`  |
| **Reassociation Requests**  | `0x2`       |  Sent by a client to request reassociation with an access point.                             | `wlan.fc.type_subtype == 2`  |
| **Resssociation Responses** | `0x3`       |  Sent by an access point in response to a reassociation request.                             | `wlan.fc.type_subtype == 3`  |
| **Probe Requests**          | `0x4`       |  Sent by a client to probe for available access points.                                      | `wlan.fc.type_subtype == 4`  |
| **Probe Responses**         | `0x5`       |  Sent by an access point in response to a probe request.                                     | `wlan.fc.type_subtype == 5`  |
| **Beacons**                 | `0x8`       |  Sent by an access point to announce its presence and provide information about the network. | `wlan.fc.type_subtype == 8`  |
| **ATIMs**                   | `0x9`       |  Sent by an access point to announce the presence of a client in power-saving mode.          | `wlan.fc.type_subtype == 9`  |
| **Disassociations**         | `0xa`       |  Sent by an access point or client to terminate an association.                              | `wlan.fc.type_subtype == 10` |
| **Authentications**         | `0xb`       |  Sent by a client to request authentication with an access point.                            | `wlan.fc.type_subtype == 11` |
| **Deauthentications**       | `0xc`       |  Sent by an access point or client to terminate an authentication.                           | `wlan.fc.type_subtype == 12` |
| **Actions**                 | `0xd`       |  Sent by a client or access point to request a specific action be taken by the other device. | `wlan.fc.type_subtype == 13` |


### Management Frames Fz3r0 Tricks & T-Shootin'

|                             **Filter**                              |                                   **Description**                                                                                       |
|:-------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------------------------------:|
| `wlan.fc.type_subtype == 0x0`                                       | Filters only Association Requests frames.                                                                                               |
| `wlan.fc.type_subtype == 0x5 && wlan.ssid == "your_SSID"`           | Filters only Probe Responses frames for a specific SSID.                                                                                |
| `wlan.fc.type_subtype == 0xb && wlan_mgt.auth.status_code != 0`     | Filters only Authentication frames with failed status code.                                                                             |
| `wlan.fc.type_subtype == 0xa && wlan.sa == "your_MAC_address"`      | Filters only Disassociation frames sent by a specific device.                       |
| `wlan.fc.type_subtype == 0x4 && !wlan_mgt.ssid`                     | Filters only Probe Requests frames that do not contain an SSID field.               |
| `wlan.fc.type_subtype == 0xd && wlan_mgt.action.category_code == 3` | Filters only Action frames with category code 3 (Spectrum Management)               |
| `wlan.fc.type_subtype == 0x0 && wlan.status_code == 2`              | Filters only association request frames with status code 2 (rejected)               |
| `wlan.fc.type_subtype == 0x3 && wlan.status_code == 1`              | Filters only reassociation response frames with status code 1 (unspecified failure) |
| `wlan.fc.type_subtype == 0x08 && wlan_mgt.rsn.akms.type == 1`       | Filters only Beacon frames that advertise WPA2-PSK security.                                                                         |
| `wlan.fc.type_subtype == 0x00 && wlan.sa == "client_mac_address"`   | Filters only Association Request frames sent by a specific client.                                                                     |
| `wlan.fc.type_subtype == 0x01 && wlan.da == "client_mac_address"`   | Filters only Association Response frames sent to a specific client.                                                             |
| `wlan.fc.type_subtype == 0x08 && wlan_mgt.rsn.akms.type == 1`       | Filters only Beacon frames that advertise WPA2-PSK security.        |
| `wlan.fc.type_subtype == 0x0b && wlan.sa == "client_mac_address"`   | Filters only Authentication frames sent by a specific client.       |
| `wlan.fc.type_subtype == 0x0b && wlan.da == "AP_mac_address"`       | Filters only Authentication frames sent to a specific AP.           |
| `eapol.keydes.type == 254`	                                      | Filters only the first EAPOL-Key frame (client -> AP)(used to initiate the 4-way handshake.)
| `eapol.keydes.type == 2`	                                          | Filters only the second EAPOL-Key frame (AP -> client) which is used to send the AP's nonce value.
| `eapol.keydes.type == 3`                                            | Filters only the third EAPOL-Key frame (client -> AP) which is used to send the client's nonce value and confirm the AP's nonce value. |
| `eapol.keydes.type == 1`	                                          | Filters only the fourth EAPOL-Key frame (AP -> client) which is used to send the Temporal Key (TK) used for encrypting data.
| `eapol`                                                             | Filters only EAPOL frames (the 4th step of the 4-way handshake)     |
| `wlan.fc.type_subtype == 0x08 || wlan.fc.type_subtype == 0x05`      | Filters the 4-Way Handshake ;) muahaha!                                     |


## Control Frames

- 802.11 `Control Frames` = `type = 1` 
- Assist with the delivery of data frames 
- Used to control and manage the flow of data on a wireless network. 
- Typically sent at a lower data rate than regular data frames and they are acknowledged by the receiving device
- They help to ensure efficient and reliable communication on a wireless network. 
- These frames are used for various purposes such as:

    - `RTS` - `Request to Send` - Request from a device the access to the wireless medium and prevent collisions between devices.
    - `CTS` - `Clear to Send` - Clearance for a device to access to the wireless medium and prevent collisions between devices.
    - `ACK` - `Acknowledgment` - To confirm the receipt of data frames by the receiving device.
    - `Block ACK` - `Various ACKs` - To confirm the receipt of multiple data frames by the receiving device.
    - `PS-Poll` - `Power Save` - To conserve power on wireless devices by allowing them to sleep when not in use.
    - `CSA` - `Channel Switch Announcement` - To inform devices of an upcoming change in the channel being used by the wireless network.

- There is a total of **8** `802.11 Control Frames`:

|        **Name**          | **Subtype**   |                                                            **Description**                                                           |    **Wireshark Filter**    |
|:------------------------:|:-------------:|:------------------------------------------------------------------------------------------------------------------------------------:|:--------------------------:|
| **`ALL CONTROL FRAMES`** | _N/A_         | This filter captures all control frames, which are used for managing the communication between stations in a wireless network.       | wlan.fc.type == 1          |
| **Block ACK request**    | `0x8`         | Block ACK request frames are used to request the receiver to send a Block ACK frame that acknowledges the receipt of multiple MPDUs. | wlan.fc.type_subtype == 24 |
| **Block ACK**            | `0x9`         | Block ACK frames are used to acknowledge the receipt of multiple MPDUs.                                                              | wlan.fc.type_subtype == 25 |
| **PS-Poll**              | `0xa`         | PS-Poll frames are used by a station in power-saving mode to request data from the AP.                                               | wlan.fc.type_subtype == 26 |
| **Ready To Send**        | `0xb`         | Ready To Send frames are used to indicate that a station is ready to receive data.                                                   | wlan.fc.type_subtype == 27 |
| **Clear To Send**        | `0xc`         | Clear To Send frames are used to indicate that a station can transmit data.                                                          | wlan.fc.type_subtype == 28 |
| **ACK**                  | `0xd`         | ACK frames are used to acknowledge the receipt of a single MPDU.                                                                     | wlan.fc.type_subtype == 29 |
| **CF-End**               | `0xe`         | CF-End frames are used to indicate the end of a contention-free period.                                                              | wlan.fc.type_subtype == 30 |
| **CF-End/CF-Ack**        | `0xf`         | CF-End/CF-Ack frames are used to indicate the end of a contention-free period and to acknowledge receipt of a single MPDU.           | wlan.fc.type_subtype == 31 |



## Data Frames

Wireless data frames are the frames used to transmit data on a wireless network. These frames are used to:

transmit data from one device to another
carry user data, such as web pages, emails, and files
Data frames are typically sent at a higher data rate than management or control frames and may be acknowledged or unacknowledged depending on the protocol used. They are essential for the actual communication on a wireless network, allowing devices to exchange information. They are typically larger in size than management or control frames as they carry the actual payload. The way data frames are handled, protected, and prioritized is a key factor in determining the overall performance and reliability of a wireless network.













## Radiotap Protocol

In Wireshark, the radiotap protocol allows to decode the contents of the radiotap header, which is a header added to frames in some wireless networks. This header contains information about the physical layer of the wireless communication, such as the signal strength, data rate, and channel frequency.

|      **Filter Name**     |                                                  **Description**                                                  |             **Example**                  |
|:------------------------:|:-----------------------------------------------------------------------------------------------------------------:|:----------------------------------------:|
| **Signal Strength**      | Filters for the signal strength in dBm (filters for frames with a signal strength greater than -80dBm)            | wlan_radio.dbm_antsignal > -80           |
| **Data Rate**            | Filters for the data rate in Mbps (filters for frames transmitted at a data rate of 12Mbps or less)               | wlan_radio.data_rate <= 12               |
| **Channel Number**       | Filters for the channel number (filters for frames transmitted on channel 1)                                      | wlan_radio.channel == 1                  |
| **Channel Flags**        | Filters for the channel flags (filters for frames transmitted on a 5GHz channel)                                  | wlan_radio.channel_flags == 0x05         |
| **Antenna**              | Filters for the antenna used for the transmission (filters for frames transmitted using antenna 1)                | wlan_radio.antenna == 1                  |
| **Frame Check Sequence** | Filters for the presence or absence of the Frame Check Sequence (FCS) (filters for frames with an FCS at the end) | wlan_radio.flags.fcs_at_end == 1         |
| **SNR**                  | Filters for the SNR in dBm (filters for frames with SNR less than 20db)                                           | wlan_radio.snr < 20                     |


## IEEE 802.11 PHY Type 

|    **802.11 PHY**    |                                       **Description**                                       | **Available Channels** |      **Filter**     |
|:--------------------:|:-------------------------------------------------------------------------------------------:|:----------------------:|:-------------------:|
| **802.11a**          | OFDM-based PHY operating in the 5GHz band                                                   | 5GHz                   | wlan_radio.phy == 0 |
| **802.11b**          | DSSS-based PHY operating in the 2.4GHz band                                                 | 2.4GHz                 | wlan_radio.phy == 1 |
| **802.11g**          | OFDM-based PHY operating in the 2.4GHz band                                                 | 2.4GHz                 | wlan_radio.phy == 2 |
| **802.11n (HT)**     | OFDM-based PHY with support for high throughput (HT) operating in the 2.4GHz and 5GHz bands | 2.4GHz, 5GHz           | wlan_radio.phy == 3 |
| **802.11ac (VHT)**   | OFDM-based PHY with support for very high throughput (VHT) operating in the 5GHz band       | 5GHz                   | wlan_radio.phy == 4 |
| **802.11ad (WiGig)** | OFDM-based PHY operating in the 60GHz band                                                  | 60GHz                  | wlan_radio.phy == 5 |
| **802.11ax (HE)**    | OFDM-based PHY with support for high efficiency (HE) operating in the 2.4GHz and 5GHz bands | 2.4GHz, 5GHz           | wlan_radio.phy == 6 |


## 802.11 Retransmissions

- Retransmission is a process of resending a frame that was not successfully received by the destination. 
- Retransmission is used to ensure that packets are delivered reliably over wireless networks. 
- Retransmission is a normal and expected process in wireless networks, but excessive retransmission can indicate a problem. 
- Some common causes of excessive retransmission include:

|                     **Filter**                     |                     **Description**                     |
|:--------------------------------------------------:|:-------------------------------------------------------:|
| wlan.fc.retry == 1                                 | Filters only retransmitted 802.11 frames.               |
| wlan.fc.retry == 1 && wlan.fc.type_subtype == 0x08 | Filters only retransmitted beacon frames.               |
| wlan.fc.retry == 1 && wlan.fc.type_subtype == 0x04 | Filters only retransmitted probe request frames.        |
| wlan.fc.retry == 1 && wlan.fc.type_subtype == 0x05 | Filters only retransmitted probe response frames.       |
| wlan.fc.retry == 1 && wlan.fc.type_subtype == 0x0b | Filters only retransmitted authentication frames.       |
| wlan.fc.retry == 1 && wlan.fc.type_subtype == 0x0c | Filters only retransmitted deauthentication frames.     |
| wlan.fc.retry == 1 && wlan.fc.type_subtype == 0x0d | Filters only retransmitted action frames.               |
| wlan.fc.retry == 1 && wlan.fc.type_subtype == 0x00 | Filters only retransmitted association request frames.  |
| wlan.fc.retry == 1 && wlan.fc.type_subtype == 0x01 | Filters only retransmitted association response frames. |


## 802.11 Frames Encryption

- Encryption can be applied to all three types of wireless frames: control, data, and management. 
- However, whether a frame is encrypted or not depends on the specific wireless protocol being used, as well as the security settings of the network.

    - `Data Frames` - **`Usually encrypted`** to protect the confidentiality and integrity of the user data they carry. 
        - This is done to ensure that only authorized devices can access the data and that the data has not been tampered with during transmission.

    - `Control frames` - **`Generally NOT encrypted`**, as they are used to manage and control the flow of data on a wireless network, rather than carrying user data. 
        - However, some advanced wireless protocols may encrypt control frames for added security.

    - `Management frames` - **`typically NOT encrypted`**, as they are used for network management and maintenance, and do not carry user data. 
        - However, some advanced wireless protocols may encrypt management frames for added security.

- It's worth noting that encryption is not always implemented, it depends on the particular network, the security policy and the level of security desired.
- You can use Wireshark's filter function to filter for encrypted or unencrypted frames of different types. Here are some examples:



To filter for encrypted 802.11 frames: wlan.fc.protected == 1
To filter for non-encrypted 802.11 frames: wlan.fc.protected == 0
To filter for control frames: wlan.fc.type == 0
To filter for management frames: wlan.fc.type == 1
To filter for data frames: wlan.fc.type == 2



You can also combine multiple filters using "and" and "or" operators, for example:

To filter for encrypted management frames: wlan.fc.protected == 1 and wlan.fc.type == 1
To filter for non-encrypted control or management frames: wlan.fc.protected == 0 and (wlan.fc.type == 0 or wlan.fc.type == 1)
You can also use the "not" operator to filter for the opposite of a given filter.






## Troubleshooting WiFi Fz3r0 Special Compliation!


|           **Filter Name**           |                        **Description**                        |                                                **Example**                                               |
|:-----------------------------------:|:-------------------------------------------------------------:|:--------------------------------------------------------------------------------------------------------:|
| **Retry flag**                      | Filters for frames that were retransmitted                    | wlan_mgt.fixed.retry == 1 (filters for frames that were retransmitted)                                   |
| **RTS/CTS flags**                   | Filters for frames that have the RTS or CTS flags set         | wlan_mgt.fixed.rts == 1 (filters for frames that have the RTS flag set)                                  |
| **Power management**                | Filters for frames that have the power management flag set    | wlan_mgt.fixed.power_mgt == 1 (filters for frames that indicate the device is in power-saving mode)      |
| **Type/Subtype**                    | Filters for frames based on their type and subtype            | wlan.fc.type == 0 && wlan.fc.subtype == 4 (filters for Beacon frames)                                    |
| **Frame Length**                    | Filters for frames based on their length                      | wlan_radio.length > 1500 (filters for frames longer than 1500 bytes)                                     |
| **Channel Utilization**             | Filters for channel utilization                               | wlan_radio.channel_utilization > 50 (filters for frames with channel utilization greater than 50%)       |
| **Packet Error Rate**               | Filters for the packet error rate                             | wlan_radio.signal_quality == 0 (filters for frames with a packet error rate of 0%)                       |
| **Transmission Rate**               | Filters for the transmission rate                             | wlan_radio.rate == 6 (filters for frames transmitted at a rate of 6Mbps)                                 |
| **Preamble Type**                   | Filters for the preamble type                                 | wlan_radio.preamble == 1 (filters for frames with a short preamble)                                      |
| **Guard Interval**                  | Filters for the guard interval                                | wlan_radio.guard_interval == 0 (filters for frames with a long guard interval)                           |
| **Beacon Interval**                 | Filters for the beacon interval                               | wlan_mgt.fixed.beacon == 100 (filters for frames with a beacon interval of 100ms)                        |
| **Maximum Transmission Unit (MTU)** | Filters for the Maximum Transmission Unit (MTU)               | wlan_radio.mcs.index == 7 (filters for frames with an MTU of 64 bytes)                                   |
| **Transmit Power**                  | Filters for the transmit power                                | wlan_radio.txpower == 20 (filters for frames transmitted with a power of 20dBm)                          |
| **Modulation Type**                 | Filters for the modulation type                               | wlan_radio.xmit_flags == 1 (filters for frames transmitted with OFDM modulation)                         |
| **Error Correcting Code**           | Filters for the error correcting code                         | wlan_mgt.fixed.error_correcting_code == 1 (filters for frames with a Reed-Solomon error correcting code) |
| **Short Guard Interval**            | Filters for frames with short guard intervals                 | wlan_mgt.fixed.short_guard_interval == 1 (filters for frames with a short guard interval)                |
| **Short Training Field**            | Filters for frames with short training fields                 | wlan_mgt.fixed.short_training_field == 1 (filters for frames with a short training field)                |
| **Spatial Streams**                 | Filters for the number of spatial streams                     | wlan_mgt.fixed.spatial_streams == 2 (filters for frames transmitted using 2 spatial streams)             |
| **Bandwidth**                       | Filters for the bandwidth of the frames                       | wlan_mgt.fixed.bandwidth == 20 (filters for frames transmitted at a bandwidth of 20MHz)                  |
| **Aggregation**                     | Filters for frames with aggregation                           | wlan_mgt.fixed.aggregation == 1 (filters for frames that are aggregated)                                 |
| **CRC Error**                       | Filters for frames with a cyclic redundancy check (CRC) error | wlan_mgt.fixed.crc_error == 1 (filters for frames with a CRC error)                                      |
| **Decryption Error**                | Filters for frames with a decryption error                    | wlan.wep.icv_bad == 1 (filters for frames with a decryption error)                                       |
| **Duplicate Frame**                 | Filters for duplicate frames                                  | wlan.seq == previous_frame_seq (filters for frames with the same sequence number as the previous frame)  |
| **Fragmentation Error**             | Filters for frames with a fragmentation error                 | wlan.fc.more_fragments == 1 (filters for frames with the "more fragments" flag set)                      |
| **FCS Error**                       | Filters for frames with a frame check sequence (FCS) error    | wlan_mgt.fixed.badfcs == 1 (filters for frames with a bad FCS)                                           |
| **Malformed Frame**                 | Filters for malformed frames                                  | frame.len < 64 (filters for frames                                                                       |
| **Retry Error**                     | Filters for frames that were retransmitted                    | wlan_mgt.fixed.retry == 1 (filters for frames that were retransmitted)                                   |
| **Duplicate Error**                 | Filters for frames that were marked as duplicates             | wlan_mgt.fixed.duplicate == 1 (filters for frames that were marked as duplicates)                        |
| **Format Error**                    | Filters for frames with a format error                        | wlan_mgt.fixed.format_error == 1 (filters for frames with a format error)                                |
| **Sequence Error**                  | Filters for frames with a sequence error                      | wlan_mgt.fixed.sequence_error == 1 (filters for frames with a sequence error)                            |
| **Length Error**                    | Filters for malformed frames                                  | frame.len < 64 (filters for frames with a length less than 64 bytes)                                     |
| **Retry Error**                     | Filters for frames that were retransmitted                    | wlan_mgt.fixed.retry == 1 (filters for frames that were retransmitted)                                   |
| **Duplicate Error**                 | Filters for frames that were marked as duplicates             | wlan_mgt.fixed.duplicate == 1 (filters for frames that were marked as duplicates)                        |
| **Format Error**                    | Filters for frames with a format error                        | wlan_mgt.fixed.format_error == 1 (filters for frames with a format error)                                |
| **Sequence Error**                  | Filters for frames with a sequence error                      | wlan_mgt.fixed.sequence_error == 1 (filters for frames with a sequence error)                            |
| **Length Error**                    | Filters for malformed frames                                  | frame.len < 64 (filters for frames with a length less than 64 bytes)                                     |
















































| **Nombre del protocolo** |                   **Significado **                  | **Puerto** | **TCP/UDP** |
|:------------------------:|:---------------------------------------------------:|:----------:|:-----------:|
| IGMP                     | Internet Group Management Protocol                  | 2          | UDP         |
| PIM-SM                   | Protocol Independent Multicast - Sparse Mode        | 103        | UDP         |
| PIM-DM                   | Protocol Independent Multicast - Dense Mode         | 104        | UDP         |
| MLD                      | Multicast Listener Discovery                        | 2          | ICMP        |
| SSM                      | Source-Specific Multicast                           | -          | -           |
| IGMPv3                   | Internet Group Management Protocol version 3        | 2          | UDP         |
| VRRP                     | Virtual Router Redundancy Protocol                  | 112        | VRRP        |
| VRRPv3                   | Virtual Router Redundancy Protocol version 3        | 112        | VRRP        |
| MSDP                     | Multicast Source Discovery Protocol                 | 639        | TCP         |
| NTP                      | Network Time Protocol                               | 123        | UDP         |
| SNMP                     | Simple Network Management Protocol                  | 161        | UDP         |
| Syslog                   | System Log Protocol                                 | 514        | UDP         |
| RTP                      | Real-time Transport Protocol                        | 5004       | UDP         |
| DHCPv6                   | Dynamic Host Configuration Protocol for IPv6        | 546        | UDP         |
| DNS                      | Domain Name System                                  | 53         | TCP/UDP     |
| mDNS                     | Multicast Domain Name System                        | 5353       | UDP         |
| ESP                      | Encapsulating Security Payload                      | 50         | ESP         |
| RTSP                     | Real Time Streaming Protocol                        | 554        | TCP         |
| SIP                      | Session Initiation Protocol                         | 5060       | TCP/UDP     |
| HSRP                     | Hot Standby Router Protocol                         | 1985       | HSRP        |
| VRRPv3-E                 | VRRP version 3 with extension headers               | 112        | VRRP        |
| RSVP                     | Resource Reservation Protocol                       | 359        | RSVP        |
| LLDP                     | Link Layer Discovery Protocol                       | 351        | LLDP        |
| STP                      | Spanning Tree Protocol                              | 329        | STP         |
| VRRPv3-M                 | VRRP version 3 with multicast                       | 112        | VRRP        |
| HSRPv2                   | Hot Standby Router Protocol version 2               | 1985       | HSRP        |
| LACP                     | Link Aggregation Control Protocol                   | 551        | LACP        |
| VRRPv3-D                 | VRRP version 3 with multicast and extension headers | 112        | VRRP        |
|                          |                                                     |            |             |



I can control the air and I can read people's minds
