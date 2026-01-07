# Context-Aware Access (CAA)

Context-Aware Access allows you to enforce granular access controls based on the identity of the user and the context of the request (device, location, security status), implementing a Zero Trust security model.

## Key Concepts
-   **Zero Trust**: Shifts access control from the network perimeter (VPNs) to the individual request.
-   **Context**: Access decisions are based on:
    -   **User Identity**: Who is requesting?
    -   **Device Posture**: Is the device managed? Encrypted? Screen-locked? OS up-to-date?
    -   **Location**: IP address or geographic region.
    -   **Third-party Signals**: Integration with CrowdStrike, VMware, etc. (Chrome Enterprise Premium).

## Use Cases
-   **Non-Employee Access**: Grant contractors access to specific web apps without a VPN.
-   **BYOD (Bring Your Own Device)**: Allow personal devices if they meet minimum security standards.
-   **DLP (Data Loss Prevention)**: Prevent copying/pasting sensitive data on unsecured devices.
-   **Geofencing**: Restrict access to specific regions.

## Integration
-   Works with **Identity-Aware Proxy (IAP)** and **VPC Service Controls** to enforce policies at the resource level.
-   **Chrome Enterprise Premium**: enhances capabilities with deep device signals and threat protection.
