# PortAppProx

## Overview

`PortAppProx` is a tool designed to automate the creation and management of a Cloudflare tunnel with DNS mapping in less than 30 seconds. It allows you to securely expose a service or application running on your server to the internet with minimal effort. The script creates a Cloudflare tunnel, sets up DNS records, configures a systemd service to manage the tunnel, and optionally starts a Python HTTP server for testing.

## Features

- **Automated Tunnel Creation**: Creates a Cloudflare tunnel using the specified name and configures it to route traffic from a given subdomain to a specified IP address and port.
- **DNS Mapping**: Sets up DNS records to map the subdomain to the Cloudflare tunnel.
- **Systemd Service Integration**: Generates a systemd service file to manage the Cloudflare tunnel, ensuring it starts on boot and can be easily managed.
- **Python HTTP Server**: Provides an option to start a temporary Python HTTP server for testing purposes.
- **Unattended Mode**: Can run in unattended mode, skipping prompts and user interactions.

![image](https://github.com/user-attachments/assets/cf386a9e-2d65-432e-b2f8-819c15b3d2f8)

![image](https://github.com/user-attachments/assets/a782de2f-7f05-45ad-9c8f-50da02392600)

![image](https://github.com/user-attachments/assets/52bd47d1-7894-48d2-9794-e3810d80d722)

![image](https://github.com/user-attachments/assets/305b9cbb-a95a-45b3-a377-f67449598bc7)

## Prerequisites (will be autoinstalled)

- **Bash**: The script requires bash to run.
- **Cloudflared**: The Cloudflare tunnel client needs to be installed. If not present, the script will install it.
- **Curl**: Used for making HTTP requests to verify the tunnel.
- **Python 3**: Required if you want to use the temporary Python HTTP server.

## Usage

```bash
./PortAppProx --name <tunnel-name> --fqdn <fqdn> --hostname <hostname> --exposed-ip <ip> --exposed-port <port> [--unattended true/false]
```

### Arguments

- `--name`: The name of the Cloudflare tunnel.
- `--fqdn`: The fully qualified domain name (FQDN) for the DNS record.
- `--hostname`: The subdomain to expose.
- `--exposed-ip`: The IP address of the service/application you want to expose.
- `--exposed-port`: The port on which the service/application is running.
- `--unattended`: Optional. If set to `true`, the script will skip prompts and run in unattended mode.

### Example

```bash
./PortAppProx --name gitlab --fqdn gitlab.example.org --hostname gitlab --exposed-ip 127.0.0.1 --exposed-port 8080 --unattended true
```

This example exposes a GitLab instance running on `127.0.0.1:8080` to `https://gitlab.example.org`.

## Installation

To use the script:

1. Clone the repository:

   ```bash
   git clone https://github.com/alexander-labarge/PortAppProx.git
   cd PortAppProx
   ```

2. Make the script executable:

   ```bash
   chmod +x PortAppProx
   ```

3. Run the script with the necessary arguments.

## Logging

The script generates a log file for each run, located in the working directory (`~/tunnel-name/`), which provides detailed information on the execution process.

## Cleanup

The script includes a cleanup function that will terminate any running Python HTTP servers started by the script. You can also choose whether to keep the server running in the background.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
