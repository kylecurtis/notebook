## Check ICMP Status

> The ping functionality is typically controlled by the **Windows Firewall**. Use the following PowerShell command to check if the firewall rule that allows ICMP Echo Requests (ping) is enabled:

<br>

#### ICMPv4 Check

Run this command to check if ICMPv4 (IPv4 ping) is enabled:

```powershell
Get-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" | Select-Object DisplayName, Enabled
```

#### ICMPv6 Check

Run this command to check if ICMPv6 (IPv6 ping) is enabled:

```powershell
Get-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv6-In)" | Select-Object DisplayName, Enabled
```

> **Note**: If `Enabled` is `True`, your computer responds to ping requests.

<br>

---

<br>

## Block Ping Requests

> To disable responding to ping requests, you can disable the relevant firewall rules:

<br>

#### For ICMPv4:

Disable ICMPv4 (IPv4 ping) by running:

```powershell
Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -Enabled False
```

#### For ICMPv6:

Disable ICMPv6 (IPv6 ping) by running:

```powershell
Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv6-In)" -Enabled False
```

<br>

---

<br>

## Block Other Identifiable Methods

> If you want to block all identifiable methods (not just ping), consider the following steps:

<br>

#### Check Your Current Network Profile:

Run the following command to check your current network profile (Private, Public, or DomainAuthenticated):

```powershell
Get-NetConnectionProfile
```

<br>

> **Explanation**: This command provides details about your active network connections, including:
> 
> - **NetworkCategory**: Indicates whether the network is `Private`, `Public`, or `DomainAuthenticated`.
> - **InterfaceAlias**: The name of the network interface (e.g., Ethernet, Wi-Fi).
> - **IPv4Connectivity**: The status of IPv4 connectivity.
> - **IPv6Connectivity**: The status of IPv6 connectivity.

<br>

---

<br>

#### Disable Network Discovery:

<br>

**Check Current Network Discovery Settings**:

```powershell
Get-NetFirewallRule -DisplayGroup "Network Discovery" | Select-Object DisplayName, Enabled
```

<br>

**Disable Network Discovery via Firewall Rules**:

```powershell
Get-NetFirewallRule -DisplayGroup "Network Discovery" | Set-NetFirewallRule -Enabled False
```

<br>

---

<br>

#### Disable File and Printer Sharing:

<br>

Disable the firewall rules for File and Printer Sharing to prevent access to shared resources:

```powershell
Set-NetFirewallRule -Group "@FirewallAPI.dll,-28502" -Enabled False
```

<br>

---

<br>

#### Block Specific Ports:

> Block ports commonly used for network discovery and sharing (e.g., TCP 445, UDP 137-138):

<br>

**Block SMB (TCP 445):**

```powershell
New-NetFirewallRule -DisplayName "Block SMB" -Direction Inbound -Protocol TCP -LocalPort 445 -Action Block
```

<br>

**Block NetBIOS (UDP 137-138):**

```powershell
New-NetFirewallRule -DisplayName "Block NetBIOS" -Direction Inbound -Protocol UDP -LocalPort 137-138 -Action Block
```

<br>

---

<br>

## Verify Firewall Rules

> After applying any changes, verify the settings:

```powershell
Get-NetFirewallRule | Where-Object { $_.Enabled -eq "True" } | Select-Object DisplayName, Direction, Enabled
```

<br>

---

<br>

## Other Firewall Settings

<br>

**Remote Assistance Rules**:

- **Examples**:
    - `Remote Assistance (RA Server TCP-In)`
    - `Remote Assistance (DCOM-In)`
- **Risk**: These rules allow external connections for remote assistance, which could be abused if the service is improperly secured or enabled without need.
- **Recommendation**: If you don't use Remote Assistance, disable these rules.

```powershell
Set-NetFirewallRule -DisplayName "Remote Assistance (RA Server TCP-In)" -Enabled False
```

<br>

**mDNS (Multicast DNS)**:

- **Examples**:
    - `mDNS (UDP-In)`
    - `mDNS (UDP-Out)`
- **Risk**: mDNS is used for device discovery (e.g., printers, smart TVs). It can reveal device information to attackers on the same network and may be used in amplification attacks.
- **Recommendation**: Disable mDNS if you don't use services like AirPlay, Chromecast, or network printers.

```powershell
Set-NetFirewallRule -DisplayName "Remote Assistance (RA Server TCP-In)" -Enabled False
```

<br>

**Connected Devices Platform**:

- **Examples**:
    - `Connected Devices Platform (UDP-In)`
    - `Connected Devices Platform (TCP-In)`
- **Risk**: This is used for sharing between devices, such as Bluetooth and Wi-Fi Direct. If not actively used, these rules expose services unnecessarily.
- **Recommendation**: Disable these rules if you don't use connected device features.

```powershell
Set-NetFirewallRule -DisplayName "Connected Devices Platform (UDP-In)" -Enabled False
```

<br>

**AllJoyn Router**:

- **Examples**:
    - `AllJoyn Router (TCP-In)`
    - `AllJoyn Router (UDP-In)`
- **Risk**: AllJoyn is an IoT communication protocol, which might not be necessary unless you have IoT devices configured to use it.
- **Recommendation**: Disable these rules if you don't have IoT devices requiring AllJoyn.

```powershell
Set-NetFirewallRule -DisplayName "AllJoyn Router (UDP-In)" -Enabled False
```

<br>

**Wi-Fi Direct Rules**:

- **Examples**:
    - `Wi-Fi Direct Network Discovery (In)`
    - `Wi-Fi Direct Scan Service Use (In)`
- **Risk**: Wi-Fi Direct is used for peer-to-peer connections without a router. If unused, it represents an unnecessary attack surface.
- **Recommendation**: Disable these rules if you don’t use Wi-Fi Direct.

```powershell
Set-NetFirewallRule -DisplayName "Wi-Fi Direct Network Discovery (In)" -Enabled False
```

<br>

**Proximity Sharing and Cast to Device**:

- **Examples**:
    - `Proximity sharing over TCP (TCP sharing-In)`
    - `Cast to Device functionality (qWave-UDP-In)`
- **Risk**: These are used for sharing files or media across devices on the same network. They can expose your system unnecessarily if not used.
- **Recommendation**: Disable these rules if you don't use these features.

```powershell
Set-NetFirewallRule -DisplayName "Proximity sharing over TCP (TCP sharing-In)" -Enabled False
```