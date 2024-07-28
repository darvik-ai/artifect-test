## Running Ansible

To run Ansible commands or playbooks, follow these general steps:

1. **Setup Inventory**: Create an inventory file (e.g., `inventory.ini`) that lists the target hosts. For example:

   ```ini
   [webservers]
   server1 ansible_host=192.168.1.10
   server2 ansible_host=192.168.1.11
   ```

2. **Run a Command**: Use the `ansible` command to execute ad-hoc commands. For example, to ping all hosts in the inventory:

   ```bash
   ansible all -i inventory.ini -m ping
   ```

3. **Execute a Playbook**: Run a playbook with the `ansible-playbook` command:

   ```bash
   ansible-playbook -i inventory.ini playbook.yml
   ```

4. **Use Extra Variables**: You can pass extra variables using the `--extra-vars` option:

   ```bash
   ansible-playbook -i inventory.ini playbook.yml --extra-vars "var1=value1 var2=value2"
   ```
