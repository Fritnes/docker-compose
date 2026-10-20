# docker-compose

Docker Compose definitions for the services below. Install Docker Engine and the
Docker Compose plugin, then run each project from its own directory:

```sh
cd <service-directory>
docker compose up -d
```

To stop a service, run `docker compose down` from the same directory. Persistent
service data is stored in bind-mounted folders under each project directory.

## Services

| Directory | Service | Ports | Upstream documentation |
| --- | --- | --- | --- |
| `gitea/` | Gitea Git hosting | `3000` (web), `222` (SSH) | [Gitea Docs](https://docs.gitea.com/) |
| `homarr/` | Homarr dashboard | `7575` (web) | [Homarr Docs](https://homarr.dev/docs/) |
| `jenkins/` | Jenkins with Ansible, Terraform, and PostgreSQL client | `8081` (web), `50000` (agent) | [Jenkins Docs](https://www.jenkins.io/doc/) |
| `nginx-proxy-manager/` | Nginx Proxy Manager | `80` (HTTP), `443` (HTTPS), `81` (admin) | [Nginx Proxy Manager Guide](https://nginxproxymanager.com/guide/) |

## Configuration

None of these Compose files requires a `.env` file. Gitea sets its container UID
and GID to `1000`; Jenkins sets `TZ` to `Europe/Kiev` in its Compose file.

Before starting Jenkins, replace `{{jenkins_ip}}` in `jenkins/docker-compose.yml`
with an available static IPv4 address on the existing external Docker network
`jenkins_vlan`. The network must already exist. Jenkins also mounts the host
Docker socket and `/usr/local/bin/docker`.

Before starting Nginx Proxy Manager, replace `{{internal_ip}}` in
`nginx-proxy-manager/docker-compose.yml` with the host IPv4 address to bind the
admin port `81` to. Its HTTP and HTTPS ports bind on all interfaces.

Gitea data, Homarr configuration and icons, Jenkins home, and Nginx Proxy Manager
data and certificates are persisted in folders mounted from their respective
service directories. Treat these folders as local service state, not source
configuration.
