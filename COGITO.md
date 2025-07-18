## Prepare dev environment
* Initialize environment variables (AWS auth and Ansible secrets)
* Activate python venv `source ~/venv/aws/bin/activate`

## View AWS Inventory
```
ansible-inventory -i inventory.aws_ec2.yml --list --yaml
```

## View Azure Inventory
```
ansible-inventory -i inventory.azure_rm.yml --list --yaml
```

## Ping Windows Hosts to Check Connectivity
```
ansible -m win_ping -i inventory.aws_ec2.yml --limit='_Windows' all
```

## AD Provisioning (likely not needed for Cogito dev)
```
# set up users and groups
ansible-playbook -i inventory.aws_ec2.yml --limit=epic-cog-sapph1.sapphire.dev playbook-provision-ad.yml
# remove computer from AD
ansible-playbook -i inventory.aws_ec2.yml --limit=epic-cog-sapph1.sapphire.dev -e computer=epic-cog-sapph1 playbook-remove-computer-ad.yml
```

## Provision Storage
```
ansible-playbook -i inventory.aws_ec2.yml --limit=tstodb playbook-provision-storage.yml
# ansible-playbook -i inventory.azure_rm.yml --limit=has_managed_disks playbook-provision-storage.yml
ansible-playbook -i inventory.azure_rm.yml --limit=clarity playbook-provision-storage.yml
```

## Install SQL
```
ansible-playbook -i inventory.aws_ec2.yml --limit=epic-cog-sapph1.sapphire.dev playbook-deploy-microsoft-sql.yml
```

## Install Cogito
```
ansible-playbook -i inventory.aws_ec2.yml --limit=epic-cog-sapph1.sapphire.dev playbook-deploy-cogito.yml
```