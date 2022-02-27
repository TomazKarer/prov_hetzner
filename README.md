# Terraform + Ansible project for self-hosted solution

## Terraform

Terraform IAAC project for provisioning server used for self-hosted solution.

At the moment it creates:

- hetzner debian 10 CX11 (1 vCPU, 2 GB RAM, 20 GB Storage) server (~3 eur/month)
- public IP (sent to Ansible inventory)
- accessible with SSH

### Prerequisites:

- secrets (../secrets):
  - Hetzner API key - created using Hetzner console
  - public SSH key (for acessing hetzner server) - created using ssh-keygen

## Ansible

Ansible playbook that creates Docker environment and needed secrets.

At the moment it:

- installs aptitute, Docker (Compose) essentials, rclone, sqlite (both used for backup), Git
- tranfers necessary secrets (sshs for install script and secrets), rclone config (this should be a part of github secrets)
- checkouts install script and secrets
- execute install procedure
- sets cron jobs for backup and renewing TLS cert

### Prerequisites:

- github:
  - install script
- secrets (../../secrets)
  - rclone config (this should be a part of github secrets)
## Usage

- `. apply.sh` - does everything
- `. ssh.sh` - sshs to provisioned server

ssh-agent bash -c 'ssh-add /root/.ssh/id_rsa.mars.github; git pull'
