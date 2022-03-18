---
title: Embedded Ansible in ManageIQ
subtitle: Ansible Automation inside ManageIQ
date: 2017-12-23
tags: [ManageIQ, Ansible]
---

ManageIQ natively supports Ansible automation since
[Fine](http://manageiq.org/blog/2017/04/Announcing-Fine-Beta-Release/)
release. So it is possible to automate resources in infrastructure or
cloud. Previously it was using Automate Datastore, for that scripts
were written in the Ruby language.

To start using Ansible inside ManageIQ, you have to enable **Embedded
Ansible** server role in configuration. It will install
ansible-tower-server without web interface. This takes time depending
upon internet speed and appliance specifications. Also, this option
uses Ansible Tower only through API.

The installation also handles creation of the database schema and we
require to retrive database password before the first run of
ansible-tower-setup. We also need a license. You can get a license on
Ansible website:
[https://www.ansible.com/license](https://www.ansible.com/license)


**Note:** It requires an Enterprise license. License is a JSON
formatted structure. We have to extend the license file to accept the
End User License Agreement(EULA): Add "eula_accepted": "true" in JSON

On
[this](http://talk.manageiq.org/t/howto-setup-embedded-ansible/2291/2)
thread, mentioned all the steps required to setup Embedded Ansible. If
you want to access Tower UI, I would suggest installing tower
separately and using Tower provider integration rather than embedded
ansible role.

I know this is a bit tedious process, to get rid of this I would
suggest to use ManageIQ Gaprindashvili release. It uses
[AWX](https://github.com/ansible/awx) instead of Ansible Tower, which
doesn't require a license.

Once you complete setup ie. installation of ansible, you need to check
EVM status for the Embedded Ansible Worker. If
[status](https://paste.opensuse.org/view/raw/90720208) of
`EmbeddedAnsibelWorker` is started, then you are done with Embedded
Ansible setup. To check, run these commands in the appliance,

```bash
$ vmdb
$ rake evm:status
```

**Note:** To see errors in this process, check evm log as:

```bash
$ vmdb; less log/evm.log
```

Once Embedded Ansile setup is done, you can add playbooks from GitHub
[repository](https://github.com/psachin/openstack-ansible-inside) to
automate.
