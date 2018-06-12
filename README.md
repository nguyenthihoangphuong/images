## 1. Project Title: **PIE**

## 2. Overview
#### 2.1 Big Picture of **PIE** system
![Big Picture](https://github.com/nguyenthihoangphuong/images/blob/Backend/PIE%20system.png?raw=true)

#### 2.2 Description:
**- Backend:** 
> The back end application which is written as micro-services for Pie Fleet that contains 4 main services: fenice, parrot, eagle, hermes

**- Frontend:**
> The front end web application for Pie Fleet. It connect to BackEnd to get/push data through APIs.

## 3. Detail System Guideline
### 3.1 Backend:
#### 3.1.1 Components in the system

**- Fenice:**
> Execute the Pie's business logic, connect database (mysql).

**- Parrot:** 
> Http gateway

**- Eagle:** 
> Connect cassandra, manage all object point: vehicle, route, leg, etc.

**- Hermes:** 
> Send messages(torilio) & email(sendgrid).

**How to save object points?**
> **Live Map:** 
> > Show position of driver job in real time. Mobile will push position to *parrot*, *fenice*. *Eagle* server will save this value on cassandra.
> > 
> > ![Object points](https://github.com/nguyenthihoangphuong/images/blob/Backend/ObjectPoint.png?raw=true)

#### 3.1.2 Installing:
> [Backend_installing](https://github.com/piemapping/backend/blob/feature/DEVOPS-244/README_BackEnd.md)

#### 3.1.3 Documents:

#### 3.1.3.1 API List:

<details>
  	<summary>Create customer</summary>
  	
  	Request:
  		POST api/v2/princessql
		body
		{
		  createCustomer(data: {
		        name: "customer1",
		        providerId: "32939f65-f6c9-4547-a61a-2083b8f3c1b5",
		        accountNumber: "123",
		        billingAddress: {
		            lineOne: "one",
		            lineTwo: "true",
		            postcode: "700000",
		            city: "hcm",
		            country: "VN"
		        },
		        contacts: [
		            {
		                firstName: "luu",
		                lastName: "quang minh",
		                email: "minh@mail.com",
		                phone: {
		                    callingCode: "84",
		                    number: "12345678"
		                }
		            }
		        ],
		        notes: "some note"
		    }) {
		    customer {
		      id
		      name
		    }
		  }
		}
	----------------------------------------------------
	Response: 
		{
		   customer {
		      id: "7e714b01-662a-406e-89fd-781a70d049e4"
		      name: "minh"
		    }
		}
	----------------------------------------------------
	Error:
	[ 
		"InvalidRequest_Error" : When missing customer's name or provider's id
		"NameInUse": When customer's name is already used
		"Database_Error": Error of server
	]
	  	
</details>
<details>
  	<summary>Update vehicle</summary>
  	
  	Request:
		mutation ($data: VehicleInput!) {
			updateVehicle(data:$data) {
				vehicle {
		            id,
		            make,
		            registrationNumber,
		            lengthMetre,
		            heightMetre,
		            widthMetre,
		            weightKilogram,
		            notes,
		            providerId,
		            locationId,
		        }
		    }
		}
		{
		    "data": {
		        "updateVehicle": {
		            "vehicle": {
		                "heightMetre": 13.65,
		                "id": "0018358e-8a76-4625-bc5a-070cedf7798d",
		                "lengthMetre": 13.65,
		                "locationId": "10099994-7f7c-48a5-bf83-173046085ac5",
		                "make": "Montracon Updated",
		                "notes": "This is note Updated",
		                "providerId": "4a3b2ac0-b3cc-11e5-af85-df26d31b15ce",
		                "registrationNumber": "307465",
		                "weightKilogram": 12000,
		                "widthMetre": 13.65
		            }
		        }
		    }
		}
  	
	----------------------------------------------------
	Response: 
		{
	    "data": {
	        "updateVehicle": {
	            "vehicle": {
	                "heightMetre": 13.65,
	                "id": "0018358e-8a76-4625-bc5a-070cedf7798d",
	                "lengthMetre": 13.65,
	                "locationId": "10099994-7f7c-48a5-bf83-173046085ac5",
	                "make": "Montracon Updated",
	                "notes": "This is note Updated",
	                "providerId": "4a3b2ac0-b3cc-11e5-af85-df26d31b15ce",
	                "registrationNumber": "307465",
	                "weightKilogram": 12000,
	                "widthMetre": 13.65
	            }
	        }
	    }
	
	----------------------------------------------------
	Error:
	[
		VehicleMissingTopLevelField:   missing object data when receiving FE request  
		VehiclePhoneEmpty:   missing phone number
		VehicleRegistrationNumberMustBeUnique:  registration number is not unique
		MaxNumberOfRegistration: registration number must be smaller than 10 characters
	]
	  	
</details>
<details>
  	<summary>API set point</summary>
  	
	Request:
	  	POST api/v2/tracking-points
		body
		{
			"point": {
			"lat": 50.93382998650727,
			"lng": -1.326139808366923
			},
			"categories": [
				{
					"type": "DRIVER",
					"value": "driver209"
				},
				{
					"type": "LEG",
					"value": "leg209"
				},
				{
					"type": "ROUTE",
					"value": "route209"
				},
				{
					"type": "VEHICLE",
					"value": "truck209"
				},
				{
					"type": "TRAILER",
					"value": "trailer209"
				}
			]
		}
  	
	----------------------------------------------------
	Response: 
	{}
	----------------------------------------------------
	Error:
	[
		"Point must have at least one category" : when body miss categories
		"CreatePoint needs a point supplied" : when body miss point
	] 	
		
</details>
<details>
  	<summary>API get last point</summary>
  	
	Request:
  	POST api/v2/graphql
	body
	{
		lastPoint(categories: [{type: "VEHICLE", value: "0f4706d6-c417-4f33-b07a-118e44c16da5"}]) {
		point
			{
				lat
				lng
				createdAt
			}
		}
	}
	----------------------------------------------------
	Response: 
	{
		"points": [
			{
				"lat": 50.93382998650727,
				"lng": -1.326139808366923,
				"createdAt": 1460988081
			},
			{
				"lat": 50.93382998650727,
				"lng": -1.326139808366923,
				"createdAt": 1460988160
			}
		]
	}
	----------------------------------------------------
	Error:
	[
		"Server internal error": when server down
	]
	  	
</details>
<details>
  	<summary>Send Email</summary>
  	
	Reference: https://sendgrid.com/docs/API_Reference/api_v3.html
	Library: https://github.com/sendgrid/sendgrid-go
	
</details>
<details>
  	<summary>SMS</summary>
  	
	Reference: https://www.twilio.com/docs/sms/send-messages
	  	
</details>

#### 3.1.3.2 Testing

> [Manual Test](https://docs.google.com/spreadsheets/d/1ToHisXyfIsDtZlo8jC60lPzzWNz8Vs0szuJJczNzkoY/edit#gid=1441377163)

> [Functional Test](https://github.com/piemapping/frontend/tree/develop/functional-test/features)

### 3.2 Frontend:
#### 3.2.1 Installing:
> [Frontend_installing](https://github.com/piemapping/backend/blob/feature/DEVOPS-244/README_FrontEnd.md)


##3. View configuration:

###3.1 Configurate dev.tfvars file:

 Link: dev/environments/fleet/config/dev.tfvars
	
	- `service_account_path`
	- `network_range`
	- `project_id`
	- `ssl_certificate_key_file`
	- `ssl_certificate_crt_file`
	- `ssl_certificate_chain_file`
	- `bootstrap_branch`
	- `subdomain`: Keep current config
	- `environment`: Keep current config
	- `instances`
	- `asg_size`
	- `services_enabled`: Turn off `crust`, `pastry`, `allinone`, `smoketests`

Get *project_id* at page:

> ![project_id](https://github.com/nguyenthihoangphuong/images/blob/CreateNewClientEnvironment/project_id.png?raw=true)

###3.2 Configurate [dev.yml](https://github.com/piemapping/infrastructure/blob/dev/environments/fleet/config/dev.yml) file:

	- Update services version (Ex: develop/lastest/v0.29.0) 
	- Get version infor at : git version of `Pie-Backend` source code.
	
###3.3 Configurate teraform.json file: 

Link file: environments/{subdomain}/service_accounts/terraform-{env}.json 

Update information as below:

	- "type"
	- "project_id"
	- "private_key_id"
	- "private_key"
	- "client_id"
	- "auth_uri"
	- "token_uri"
	- "auth_provider_x509_cert_url"
	- "client_x509_cert_url"
	
###3.4 Configurate {env}.sh file 

	- Link file: environments/{subdomain}/{env}.sh 
	- Grant +x

###3.5 File ansible.yml

Target config this file:

	- Include credential
	- sql: config connect to Database server
	- elastic search: index - each client has different index configuration
	- pusher: third party to notification

> ![Pusher](https://github.com/nguyenthihoangphuong/images/blob/CreateNewClientEnvironment/pusher.png?raw=true)

**Config ansible.yml file  for 2 cases: (single-tenancy) or (multi-tenancy):**

> - *single-tenancy*: ansible/roles/consul-configuration/vars/{project_id}.yml
> - *multi-tenancy*: ansible/roles/consul-configuration/vars/customer-{env}/{subdomain}.yml

	
##4. Push to repository:

- Run teraform 	
> cd workspace/go/src/github.com/piemapping/infrastructure/terraform
> terraform env new {subdomain}-{env}
> > ex: terraform env new fleet-dev

- terraform plan to check {env}.tfvars file
- Run teraform to create platform
- terraform apply
- Result:
![Terraform successful](https://github.com/nguyenthihoangphuong/images/blob/CreateNewClientEnvironment/Terraform%20Successful.png?raw=true)

##5. Config DNS

- Go to google domain: https://domains.google.com/
- Config DNS 
![DNS](https://github.com/nguyenthihoangphuong/images/blob/CreateNewClientEnvironment/DNS.png?raw=true)
