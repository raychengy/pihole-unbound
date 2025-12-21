# Pi-hole with Unbound and Cloudflare Tunnel

This project sets up a Pi-hole instance with a local recursive DNS resolver (Unbound) and exposes the web interface securely over the internet using a Cloudflare Tunnel.

## Services

*   **Pi-hole:** A network-wide ad blocker.
*   **Unbound:** A secure, recursive, and caching DNS resolver.
*   **Cloudflare Tunnel:** A secure tunnel to expose the Pi-hole web interface.

## Prerequisites

*   Docker
*   Docker Compose

## Configuration

1.  **Clone the repository or download the files.**

2.  **Create an `.env` file:**
    Create a file named `.env` in the same directory as the `docker-compose.yml` file. You can copy the `.env.example` file:
    ```bash
    cp .env.example .env
    ```
    Then, edit the `.env` file and set the following variables:
    *   `TZ`: Your timezone (e.g., `America/New_York`).
    *   `WEBPASSWORD`: A password for the Pi-hole web interface.
    *   `TUNNEL_TOKEN`: Your Cloudflare Tunnel token.
    *   `PIHOLE_IP`: The static IP for your Pi-hole (e.g., `192.168.1.200`).
    *   `PIHOLE_LAN_PARENT`: The name of your host's main network interface (e.g., `eth0`). Find it with `ip addr`.
    *   `PIHOLE_LAN_SUBNET`: Your local network's subnet (e.g., `192.168.1.0/24`).
    *   `PIHOLE_LAN_GATEWAY`: Your router's IP address (e.g., `192.168.1.1`).

3.  **Configure Cloudflare Tunnel:**
    The `cloudflare-tunnel` service in the `docker-compose.yml` is configured to use the token from your `.env` file. You need to have a tunnel created in your Cloudflare Zero Trust dashboard. The tunnel's private network service should be configured to point to `http://pihole:80`.

## Usage

1.  **Start the services:**
    ```bash
    docker-compose up -d
    ```

2.  **Accessing the Pi-hole Web Interface:**
    You can access the Pi-hole web interface through the public hostname you configured for your Cloudflare Tunnel.

3.  **Using Pi-hole as your DNS Server:**
    To start blocking ads, you need to configure your devices (or your router) to use the Pi-hole's IP address as their DNS server. Based on the default `docker-compose.yml`, the IP address is `192.168.1.200`.

## Stopping the services

To stop the services, run:
```bash
docker-compose down
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.