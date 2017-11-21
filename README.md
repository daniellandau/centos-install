# Personal server installation

```sh
cp inventory-template.ini inventory.ini
ansible-galaxy install geerlingguy.repo-epel --roles-path roles
ansible-galaxy install geerlingguy.repo-remi --roles-path roles
ansible-galaxy install thefinn93.letsencrypt --roles-path roles
ansible-galaxy install bertvv.mariadb --roles-path roles
ansible-galaxy install kyl191.openvpn --roles-path roles
ansible-playbook email.yml -i inventory.ini --ask-become-pass
ansible-playbook openvpn.yml -i inventory.ini --ask-become-pass
ansible-playbook misc.yml -i inventory.ini --ask-become-pass
ansible-playbook web.yml -i inventory.ini --ask-become-pass
```

* Set up SPF and DKIM text records
  * DKIM record can be found in /etc/opendkim/keys/mail.txt
* Download and extract (as user nginx) Nextcloud to {{ data_mount }}/webapps
  * Set up database passwords in config/config.php manually (Nextcloud version is included in that file, so can't manage it with ansible)
  * Restore database manually if migrating from another computer


### Notes

* Installing OpenVPN didn't work with just the playbook for my purposes as I want to be able to talk from server to clients. After running playbook, do `sudo iptables-save | sudo tee /etc/sysconfig/iptables`, edit the row with `s/-j SNAT --to-source IP-ADDRESS/-j MASQUERADE/` and `sudo cat /etc/sysconfig/iptables | sudo iptables-restore`. The role might support this in the future: https://github.com/kyl191/ansible-role-openvpn/issues/50
