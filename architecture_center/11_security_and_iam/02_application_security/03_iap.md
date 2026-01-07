# Identity-Aware Proxy (IAP)

Identity-Aware Proxy (IAP) is a global service that controls access to your cloud applications and VMs running on Google Cloud, verifying user identity and context for every request.

## How It Works
1.  **Interception**: IAP intercepts requests sent to your application (App Engine, Cloud Run, Compute Engine) or VM (via SSH/RDP).
2.  **Authentication**: Checks for valid credentials (Google Account/Workspace). If missing, redirects to sign-in flow (OAuth 2.0).
3.  **Authorization**: Checks if the authenticated user has the necessary IAM role (e.g., `IAP-secured Web App User`).
4.  **Context Check**: Applies any Context-Aware Access levels (device posture, IP) if configured.

## Key Benefits
-   **No VPN Required**: Enables secure remote access to internal apps and VMs over the internet.
-   **Centralized Control**: Manage access via IAM policies rather than network firewalls.
-   **Protection**: Shields your application from unauthorized access and DDoS attacks (requests are stopped at the proxy before reaching your app).

## Supported Resources
-   **Web Apps**: App Engine, Cloud Run (via Load Balancer or direct), Compute Engine (via Load Balancer).
-   **VM Administration**: Secure SSH and RDP access to VMs (tunneling through IAP) without exposing public IP addresses.
