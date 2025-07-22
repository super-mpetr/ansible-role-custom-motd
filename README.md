# Ansible Role: Custom MOTD

[![Lint Ansible Role](https://github.com/super-mpetr/ansible-role-custom-motd/actions/workflows/lint.yml/badge.svg)](https://github.com/super-mpetr/ansible-role-custom-motd/actions/workflows/lint.yml)

This Ansible role configures a **custom Message of the Day (MOTD)** on Linux servers, displayed upon SSH login.

## Features

- Prompts user for a custom welcome message at runtime
- Displays the message using ASCII art via `figlet`
- Fully idempotent and lint-checked
- Supports Debian and Ubuntu platforms

---

## Requirements

- Ansible ≥ 2.12
- `figlet` package (automatically installed by the role)

---

## Role Variables

No variables need to be defined in advance. You will be prompted when running the playbook.

| Variable              | Description                               | Default                   |
|-----------------------|-------------------------------------------|---------------------------|
| `custom_motd_message` | The welcome message to display on login   | `Welcome to the server!`  |

---

## Example Playbook

```yaml
- name: Run custom MOTD role
  hosts: all
  become: true

  vars_prompt:
    - name: custom_motd_message
      prompt: "Enter your custom SSH welcome message"
      private: false

  pre_tasks:
    - name: Set default motd_message if empty
      ansible.builtin.set_fact:
        custom_motd_message: "{{ custom_motd_message | default('') | trim }}"
    - name: Apply default welcome message if input empty
      ansible.builtin.set_fact:
        custom_motd_message: "{{ custom_motd_message | default('Welcome to the server!') }}"

  roles:
    - custom_motd
```

## License

MIT

## Author Information

This role was created by **super-mpetr**.