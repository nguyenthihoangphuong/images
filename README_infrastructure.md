#How to setup *Develoment* environment
##1. Create accounts:
###1.1  Init VM instances in Google Cloud:

Go to Compute Enginers > VM instances

> ![VM instances](https://github.com/nguyenthihoangphuong/images/blob/CreateNewClientEnvironment/VM%20instances.png?raw=true)


###1.2  Create Service account in AIM & admin:

Go to AIM & admin, create account service, configuration files on Teraform

> ![VM instances](https://github.com/nguyenthihoangphuong/images/blob/CreateNewClientEnvironment/AIM%20&%20admin,%20create%20account%20service.png?raw=true)

Grant project owner

> ![VM instances](https://github.com/nguyenthihoangphuong/images/blob/CreateNewClientEnvironment/grant%20project%20owner.png?raw=true)

###2.  Go to stack driver
###3. View configuration:
###3.1 Configurate [dev.tfvars](https://github.com/piemapping/infrastructure/blob/dev/environments/fleet/config/dev.tfvars) file:
	
	- `service_account_path`
	- `network_range`
	- `project_id`
> ![project_id](https://github.com/nguyenthihoangphuong/images/blob/CreateNewClientEnvironment/project_id.png?raw=true)

	- `ssl_certificate_key_file`
	- `ssl_certificate_crt_file`
	- `ssl_certificate_chain_file`
	- `bootstrap_branch`
	- `subdomain`: Keep current config
	- `environment`: Keep current config
	- `instances`
	- `asg_size`
	- `services_enabled`: Turn off `crust`, `pastry`, `allinone`, `smoketests`

###3.2 Configurate [dev.yml](https://github.com/piemapping/infrastructure/blob/dev/environments/fleet/config/dev.yml) file:

	Update services version (develop/lastest/v0.29.0) - git version of `Pie-Backend` source code.
	
###3.3 Configurate service_accounts.json 
<mark>Slack</mark> teraform.json file: environments/{subdomain}/service_accounts/terraform-{env}.json 
	
###3.4 file {env}.sh => environments/{subdomain}/{env}.sh <mark>Slack</mark>
Grant +x

###3.5 File ansible.yml
Target config this file:

- Include credential
- sql: config connect to Database server
- pusher: third party to notification

> ![Pusher](https://github.com/nguyenthihoangphuong/images/blob/CreateNewClientEnvironment/pusher.png?raw=true)

- elastic search: index - each client has different index configuration

**Config ansible.yml file  for 2 cases: (single-tenancy) or (multi-tenancy):**

> - *single-tenancy*: ansible/roles/consul-configuration/vars/{project_id}.yml
> - *multi-tenancy*: ansible/roles/consul-configuration/vars/customer-{env}/{subdomain}.yml

	
###4. Push to repository:

- Run teraform 	
> cd workspace/go/src/github.com/piemapping/infrastructure/terraform
> terraform env new {subdomain}-{env}
> > ex: terraform env new fleet-dev

- terraform plan to check {env}.tfvars file
- Run teraform to create platform
- terraform apply
- Result:
![Terraform successful](https://github.com/nguyenthihoangphuong/images/blob/CreateNewClientEnvironment/Terraform%20Successful.png?raw=true)

###5. Config DNS

- Go to google domain: https://domains.google.com/
- Config DNS 
![DNS](https://github.com/nguyenthihoangphuong/images/blob/CreateNewClientEnvironment/DNS.png?raw=true)
	
	
	