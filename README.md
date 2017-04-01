# Personal server installation

```sh
cp inventory-template.ini inventory.ini
ansible-galaxy install geerlingguy.repo-epel --roles-path roles
ansible-galaxy install geerlingguy.repo-remi --roles-path roles
ansible-galaxy install thefinn93.letsencrypt --roles-path roles
ansible-galaxy install bertvv.mariadb --roles-path roles
ansible-playbook email.yml -i inventory.ini --ask-become-pass
ansible-playbook misc.yml -i inventory.ini --ask-become-pass
ansible-playbook web.yml -i inventory.ini --ask-become-pass
```

* Set up SPF and DKIM text records
  * DKIM record can be found in /etc/opendkim/keys/mail.txt
* Download and extract (as user nginx) Nextcloud to {{ data_mount }}/webapps
  * Set up database passwords in config/config.php manually (Nextcloud version is included in that file, so can't manage it with ansible)
  * Restore database manually if migrating from another computer
