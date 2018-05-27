#How to setup *Develoment* environment
##1. Create accounts:
###1.1  Init VM instances in Google Cloud:

> Go to Compute Enginers > VM instances
> 
> ![VM instances](https://github.com/nguyenthihoangphuong/images/blob/CreateNewClientEnvironment/2.1.png?raw=true)

###1.2  Create Service accout in AIM & admin:
###aaaaaaaaaaaaa
####aaaaaaaaaaa
#####aaaaaaaaaaaaaaaa
######aaaaaaaaaaaaaaa


1. Go to AIM & admin, create account service, configuration files on Teraform and grant project owner
2. Go to stack driver
3. Remove default nextwork
4. View configuration:

	4.1 Configurate [dev.tfvars](https://github.com/piemapping/infrastructure/blob/dev/environments/fleet/config/dev.tfvars) file:
	
- `service_account_path`
- `network_range`
- `project_id` <mark>Hinh tham khao</mark>
- `ssl_certificate_key_file`
- `ssl_certificate_crt_file`
- `ssl_certificate_chain_file`
- `bootstrap_branch`
- `subdomain`: Keep current config
- `environment`: Keep current config
- `instances`
- `asg_size`
- `services_enabled`: Turn off `crust`, `pastry`, `allinone`, `smoketests`

	4.2 Configurate [dev.yml](https://github.com/piemapping/infrastructure/blob/dev/environments/fleet/config/dev.yml) file 
	Update services version (develop/lastest/v0.29.0) - git version of `Pie-Backend` source code.
	
	4.3 Configurate service_accounts.json <mark>Slack</mark>
	teraform.json file
	
	4.4 File .sh  <mark>Slack</mark>
Grant +x

	4.5 File ansible.yml
	Target:
	Include credential
	sql: config connect to Database server
	pusher: third party to notification <mark>Slack</mark>
	elastic search: index - each client has different index configuration
	* Go to site to configuration environment
	
5. Push to repository
Run teraform 
cd .../teraform <mark>Slack</mark>
Run teraform to create platform
In process: new, plan, apply
Result: <mark>Slack</mark>

6. Config DNS
<mark>Slack</mark>
	
	
	