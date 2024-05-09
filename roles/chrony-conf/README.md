# Ansible Role: chrony-conf

This Ansible role configures Chrony and installs Chrony on target hosts. It dynamically sets the NTP servers based on the domain name of the target host.

## Task Breakdown

- `Set Chrony configuration`: Sets the Chrony configuration using a Jinja2 template located at `templates/chrony.conf.j2`, with the `fqdn` variable passed as a parameter.
- `Install Chrony`: Installs the Chrony package using the package manager.

## Handlers

- `Restart Chrony`: Restarts the Chrony service when triggered, ensuring that changes to the configuration take effect.

## Prerequisites

- Ansible installed on the control node.
- SSH access to the target hosts with sudo privileges.

## Usage

1. Clone this repository to your Ansible project:

    ```bash
    git clone <repository-url>
    ```

2. Include the `chrony-conf` role in your playbook's roles section:

    ```yaml
    roles:
      - role: chrony-conf
    ```

3. Customize any variables in `templates/chrony.conf.j2` and `chrony-conf` file if needed.

4. Run your playbook.

## Dynamic NTP Server Configuration

The role dynamically sets the NTP servers based on the domain name of the target host. Depending on the domain, it configures the appropriate NTP servers.


- **Example:**
  - For hosts ending with `o-dc.ba.uwv.nl`, it sets NTP servers to `10.178.128.21` and `10.178.128.22`.
  - For hosts ending with `t-dc.ba.uwv.nl`, it sets NTP servers to `10.178.128.18` and `10.178.128.19`.
  - For hosts ending with `a-dc.ba.uwv.nl`, it sets NTP servers to `10.178.128.15` and `10.178.128.16`.
  - For hosts ending with `p-dc.ba.uwv.nl`, it sets NTP servers to `10.178.128.10` and `10.178.128.12`.

