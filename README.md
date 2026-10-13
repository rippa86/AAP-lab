# AAP-lab
# Training Lab: System Audit & Reporting

## Objective
This playbook gathers system facts, generates a customized text report using a Jinja2 template, and exports hardware metrics to Ansible Automation Platform (AAP) for downstream use.

## Required Variables
These variables are currently commented out and **must** be provided at runtime (via `--extra-vars`, inventory, or AAP survey) for the playbook to succeed:
* `env_name`: The environment (e.g., "development")
* `user_name`: The target owner (e.g., "david")
* `dest_path`: The report save location (e.g., `/tmp/{{ user_name }}_report.txt`)

## Task Workflow
1. **Connectivity Check:** Pings the host and displays a banner with OS and hostname.
2. **Template Generation:** Uses `ansible.builtin.template` to create a report from `templates/system_report.j2`.
3. **Validation:** Reads the file using the `command` module (`cat`) and prints it to the console via `debug`.
4. **AAP Integration:** Uses `ansible.builtin.set_stats` to expose vCPU, Memory, and OS variables to subsequent workflow nodes in AAP/AWX.

## 🛠️ Exercise Fixes / Best Practices
Students should identify and fix the following issues in the provided code:
* **FQCN:** Change the bare `ping:` module to `ansible.builtin.ping:`.
* **Idempotency:** Replace the `command: cat` task with `ansible.builtin.slurp` or a `lookup` plugin to natively read file contents without shell commands.
* **YAML Syntax:** Fix the errant hyphens (`-`) inside the `msg` block of the final debug task.
