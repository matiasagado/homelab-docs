# Ubuntu LTS Installation on Dell XPS

**Date:** 2026-03-25  
**Machine:** Dell XPS 15 9510
**OS Version:** Ubuntu 24.04.4 LTS

## Linux Installation

1. Downloaded Ubuntu LTS ISO.
2. Created bootable USB with belenaEtcher.
3. Installed Ubuntu:
   - Partition layout: default partitioning
   - File system: ext4

## Initial Configuration

1. Installed updates

```bash
sudo apt update && sudo apt upgrade
```

2. Installed essential tools:

```bash
sudo apt install git curl wget build-essential htop tree net-tools unzip -y
```

3. Enabled Firewall

```bash
sudo ufw allow OpenSSH
sudo ufw enable
sudo ufw status
```

4. Installed, enabled, and verfied SSH server:

```bash
sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh
ssh matiasagado@127.0.0.1
```

## SSH Prompt Customization

1. show `(ssh)` in terminal only during SSH sessions

```bash
# ~/.bashrc
if [ -n "$SSH_CONNECTION" ] && [ -n "$SSH_TTY" ]; then
    PS1="(ssh) $PS1"
fi
```

2. Problems Encountered:

- Initial PS1 overrides color prompt
- Some leftover session variable caused incorrect prompt

## Docker Installation

1. Docker engine installed manually: version 28.2.2

```bash
sudo mkdir -p /usr/local/lib/docker/cli-plugins
sudo curl -SL https://github.com/docker/compose/releases/download/v2.20.2/docker-compose-linux-x86_64 -o /usr/local/lib/docker/cli-plugins/docker-compose
sudo chmod +x /usr/local/lib/docker/cli-plugins/docker-compose
docker compose version
```

2. Docker Compose Issue:

- `docker compose` unkown command
- Ubuntu package `docker-compose` old (v.1.19.2)

3. Add user to Docker group:

```bash
sudo usermod -aG docker $USER
newgrp docker
```

4. Tested docker

```bash
docker run hello-world
```

## Problems & Fixes

## Problems & Fixes

| Problem                                  | What Went Wrong                                         | How I Fixed It                                                        |
| ---------------------------------------- | ------------------------------------------------------- | --------------------------------------------------------------------- |
| SSH prompt not showing `(ssh)` correctly | PS1 override removed colors; leftover env vars          | Added SSH-aware PS1 with `$PS1` prepend                               |
| Docker Compose command not found         | Ubuntu package outdated, default repo missing v2 plugin | Installed Compose v2 manually in `/usr/local/lib/docker/cli-plugins/` |
| Permission denied running Docker         | User not in Docker group                                | Added user to Docker group, ran `newgrp docker`                       |
| Old docker-compose conflicts             | Ubuntu repo installs v1.19.2                            | Removed old package after installing v2                               |

## Notes
