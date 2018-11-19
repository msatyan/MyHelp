

### [Managed Service Identity (MSI) for Azure:](https://docs.microsoft.com/en-us/azure/active-directory/managed-service-identity/overview)

Managed Service Identity provides Azure services with a managed identity in Azure Active Directory. You can use this identity to authenticate to services that support Azure AD authentication, without needing credentials in your code.  

Managed Service Identity comes with Azure Active Directory Free, which is the default for Azure subscriptions. There is no additional cost for Managed Service Identity.

There are two types of Managed Service Identities available: System Assigned and User Assigned.

#### System Assigned 
A System Assigned MSI is enabled directly on an Azure service instance. Through the enable process, Azure creates an identity for the service instance in the Azure AD tenant, and provisions the credentials for the identity onto the service instance. The life cycle of a system assigned MSI is directly tied to the Azure service instance it's enabled on. If the service instance is deleted, Azure automatically cleans up the credentials and the identity in Azure AD.

#### User Assigned
A User Assigned MSI (private preview) is created as a standalone Azure resource. Through the create process, Azure creates an identity in the Azure AD tenant. After the identity is created, it can be assigned to one or more Azure service instances. Since a user-assigned MSI can be used by multiple Azure service instances, it's life cycle is managed separately.



### Short note
- Azure Resource Manager receives a message to enable the system-assigned MSI on a VM.  

- Azure Resource Manager creates a Service Principal in Azure AD to represent the identity of the VM. The Service Principal is created in the Azure AD tenant that is trusted by this subscription.  

- Azure Resource Manager configures the Service Principal details in the Azure Instance Metadata Service (IMDS) of the VM. This step includes configuring client ID and certificate used by the IMDS to get access tokens from Azure AD.  

- Now that the Service Principal identity of the VM is known, it can be granted access to Azure resources. For example, if your code needs to call Azure Resource Manager, then you would assign the VM’s Service Principal the appropriate role using Role-Based Access Control (RBAC) in Azure AD. If your code needs to call Key Vault, then you would grant your code access to the specific secret or key in Key Vault.  

- Your code running on the VM requests a token from IMDS identity endpoint: http://169.254.169.254/metadata/identity/oauth2/token. The resource parameter specifies the service to which the token is sent. For example, if you want your code to authenticate to Azure Resource Manager, you would use resource=https://management.azure.com/.  

- The MSI IMDS uses its configured client ID and certificate to request an access token from Azure AD. Azure AD returns a JSON Web Token (JWT) access token.  

- Your code sends the access token on a call to a service that supports Azure AD authentication.

### AZ CLI: Create a VM with MSI enabled
```bash
# create resource group
az group create --name myResourceGroup1 --location eastus

# Create a VM
az vm create -n myVm1 -g MyResourceGroup1 --image Centos

# Enable Managed Service Identity (MSI) on the VM
az vm identity assign -g myResourceGroup1 -n myVm1

# FYI: Delete resource group (by any chance)
# az group delete --name myResourceGroup1
```


### local MSI endpoint to get an access token
```bash
# Get an access token 
curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/' -H Metadata:true

# Then validate with the Access token (JWT)
curl -X GET -H "Authorization: Bearer <JWT token here>" -H "Content-Type: application/json"  "https://management.azure.com/tenants/?api-version=2018-02-01"
```

#### output 
```json
{
    "access_token": "<The Actual JWT>",
    "client_id": "d5ef6929-7f82-48d3-98e1-a7f1ec7a3f06",
    "expires_in": "3599",
    "expires_on": "1524630031",
    "ext_expires_in": "0",
    "not_before": "1524626131",
    "resource": "https://management.azure.com/",
    "token_type": "Bearer"
}

```

#### The JWT token from myVM1 
```json
{
  "typ": "JWT",
  "alg": "RS256",
  "x5t": "FSimuFrFNoC0sJXGmv13nNZceDc",
  "kid": "FSimuFrFNoC0sJXGmv13nNZceDc"
}

// .
// from VM1
{
  "aud": "https://management.azure.com/",
  "iss": "https://sts.windows.net/189de737-c93a-4f5a-8b68-6f4ca9941912/",
  "iat": 1524626131,
  "nbf": 1524626131,
  "exp": 1524630031,
  "aio": "Y2dgYNANujPH8Wj/otdHV72IrmQ7AwA=",
  "appid": "d5ef6929-7f82-48d3-98e1-a7f1ec7a3f06",
  "appidacr": "2",
  "idp": "https://sts.windows.net/189de737-c93a-4f5a-8b68-6f4ca9941912/",
  "oid": "465a6435-389e-4e39-b428-0d3c4044e7a2",
  "sub": "465a6435-389e-4e39-b428-0d3c4044e7a2",
  "tid": "189de737-c93a-4f5a-8b68-6f4ca9941912",
  "uti": "Nuu2I6Vx9k-2icPV-BdTAA",
  "ver": "1.0"
}
```


 myVM2
```json
{
  "aud": "https://management.azure.com/",
  "iss": "https://sts.windows.net/189de737-c93a-4f5a-8b68-6f4ca9941912/",
  "iat": 1524626579,
  "nbf": 1524626579,
  "exp": 1524630479,
  "aio": "Y2dgYLg15Zrnf5bY/Y/unQl4dWPhCQA=",
  "appid": "524ed2c4-a8f3-4b64-9cb9-398a8b867154",
  "appidacr": "2",
  "idp": "https://sts.windows.net/189de737-c93a-4f5a-8b68-6f4ca9941912/",
  "oid": "12249ec9-cc2a-47e9-9cec-579881f81a6b",
  "sub": "12249ec9-cc2a-47e9-9cec-579881f81a6b",
  "tid": "189de737-c93a-4f5a-8b68-6f4ca9941912",
  "uti": "9Egka4wHzEOLAscislIVAA",
  "ver": "1.0"
}
```



- aud  
Audience of the token. When the token is issued to a client application, the audience is the client_id of the client.

- iss  
Identifies the token issuer

- iat  
Issued at time. The time when the JWT was issued. The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token was issued.

- nbf  
Not before time. The time when the token becomes effective. For the token to be valid, the current date/time must be greater than or equal to the Nbf value. The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token was issued.

- exp  
Expiration time. The time when the token expires. For the token to be valid, the current date/time must be less than or equal to the exp value. The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token validity expires.

- oid  
Object identifier (ID) of the user object in Azure AD.

- sub  
The subject of the token, which is the unique ID for the service account that you associated with your instance. **This is a persistent and immutable identifier for the user that the token describes**. Use this value in caching logic.

- tid  
Tenant identifier (ID) of the Azure AD tenant that issued the token.

- ver  
Version. The version of the JWT token, typically 1.0.



#### Authorize

* [ Authorize access to web applications using OAuth 2.0 and Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-protocols-oauth-code)
* [Tenants - List](https://docs.microsoft.com/en-us/rest/api/resources/tenants/list)


#### Validate the Tenant
```bash 
# Then validate with the Access token (JWT)
curl -X GET -H "Authorization: Bearer <JWT token here>" -H "Content-Type: application/json"  "https://management.azure.com/tenants/?api-version=2018-02-01"
```

Output is 
```json
{
    "value": [
        {
            "id": "/tenants/189de737-c93a-4f5a-8b68-6f4ca9941912",
            "tenantId": "189de737-c93a-4f5a-8b68-6f4ca9941912"
        }
    ]
}
```



### FYI
* [Managed Service Identity (MSI) for Azure resources](https://docs.microsoft.com/en-us/azure/active-directory/managed-service-identity/overview)

* [How to use Azure Managed Service Identity ](https://docs.microsoft.com/en-us/azure/app-service/app-service-managed-service-identity)
* [Azure REST API Reference](https://docs.microsoft.com/en-us/rest/api/)
* [REST API: Azure Resource Manager](https://docs.microsoft.com/en-us/rest/api/resources/)
* [Use Resource Manager authentication API to access subscriptions](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-api-authentication)
* [Understand : Azure Resource Manager templates](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates?toc=%2Fazure%2Fazure-resource-manager%2Ftoc.yml)

* [Authorize using OAuth 2.0 and Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-protocols-oauth-code)
* [Azure Active Directory v2.0 and the OAuth 2.0 client credentials flow](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-protocols-oauth-client-creds)
* [Azure Active Directory v2.0 authentication libraries](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-libraries)

* [Azure Hypervisors tag](https://github.com/Azure/azure-linux-extensions/blob/master/AzureEnhancedMonitor/hvinfo/src/hvinfo.c)  
MS VM: Chassis Asset Tag field in dmidecode output :  “7783-7084-3265-9085-8269-3286-77” This corresponds to “MSFT AZURE VM”
