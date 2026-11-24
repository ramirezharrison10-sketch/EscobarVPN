# Escobar SSH & V2Ray VPN — Android starter

This Android Studio starter provides an Android UI/profile editor for SSH and V2Ray-style profiles and parsing of VMess and VLESS URI fields. It is **not yet a functioning VPN**: it has no integrated packet-forwarding engine. A `VpnService` alone is not a VPN tunnel; a backend must consume the TUN file descriptor, forward packets, protect its upstream sockets from VPN routing loops, and handle DNS, errors, and lifecycle correctly.

## Features in this prototype
- Kotlin Android app; min API 26
- SSH profile fields (host, port, username, password)
- VMess URI parsing (base64 JSON)
- VLESS URI parsing (host, port, user ID, fragment)
- Save/list profiles locally (prototype storage is **not encrypted**; don't store real credentials yet)
- `VpnService` integration boundary in `TunnelVpnService.kt`

## Build
1. Install Android Studio on a computer.
2. Extract this ZIP and open the `EscobarVPN` folder.
3. Allow Gradle sync; install the Android SDK for compile SDK 35 if prompted.
4. Build > Build APK(s). The project should produce a debug APK if the SDK/Gradle setup is valid.

## Next backend integration step
Use a maintained, audited Android-compatible core/library for V2Ray-compatible protocols (such as a supported sing-box or V2Ray Android integration) and a maintained SSH tunnel implementation. Check each project's license, Android build instructions, release status, and security model. Connect the engine's TUN reader/writer to the VPN service; don't establish routes before the engine is ready. Implement encrypted profile storage (Android Keystore), SSH host-key verification, IPv4/IPv6, DNS, reconnection, and clear failure handling before real use.

## Safety/security notes
- Never trust a server just because a connection succeeds. Verify SSH host keys.
- Treat imported V2Ray links as sensitive; they can contain credentials.
- This starter is not designed to bypass provider restrictions or to conceal malicious traffic.
