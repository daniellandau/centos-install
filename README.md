# Personal server installation

```sh
cp inventory-template.ini inventory.ini
ansible-galaxy install geerlingguy.repo-epel --roles-path roles
ansible-galaxy install thefinn93.letsencrypt --roles-path roles
ansible-playbook email.yml -i inventory.ini --ask-become-pass
```

* Set up SPF and DKIM text records
  * DKIM record can be found in /etc/opendkim/keys/mail.txt
