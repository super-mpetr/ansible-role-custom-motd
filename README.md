# Ansible Role: Custom MOTD

[![Lint Ansible Role](https://github.com/super-mpetr/ansible-role-custom-motd/actions/workflows/lint.yml/badge.svg)](https://github.com/super-mpetr/ansible-role-custom-motd/actions/workflows/lint.yml)[![Molecule Test](https://github.com/super-mpetr/ansible-role-custom-motd/actions/workflows/molecule.yml/badge.svg)](https://github.com/super-mpetr/ansible-role-custom-motd/actions/workflows/molecule.yml)

This Ansible role configures a **custom Message of the Day (MOTD)** on Linux servers, displayed upon SSH login.

## Features

- Displays a custom welcome message on SSH login using ASCII art (`figlet`)
- Fully idempotent and lint-checked
- Supports Debian and Ubuntu platforms

---

## Requirements

- Ansible ≥ 2.12
- `figlet` package (automatically installed by the role)

---

## Role Variables

| Variable              | Description                               | Default                   |
|-----------------------|-------------------------------------------|---------------------------|
| `custom_motd_message` | The welcome message to display on login   | `"Welcome to the server!"`|

Default value can be overridden in your playbook or inventory.

---

## Installation

You can install the role from Ansible Galaxy:

```bash
ansible-galaxy role install super-mpetr.custom_motd
```

## Usage
```yaml
- name: Configure custom MOTD
  hosts: all
  become: true

  vars:
    custom_motd_message: "Hello from Ansible!"

  roles:
    - super-mpetr.custom-motd
```

### **Optional:** Prompt for message during playbook run

If you want to prompt the user to enter the message interactively, you can add:

```yaml
vars_prompt:
  - name: custom_motd_message
    prompt: "Enter your custom SSH welcome message"
    private: false
```

to your playbook before including the role.

## Testing

This role includes Molecule tests for validation. Run tests locally with:

```bash
molecule test
```

## License

MIT

## Author Information

This role was created by **super-mpetr**.