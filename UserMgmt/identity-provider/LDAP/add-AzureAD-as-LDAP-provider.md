

### Enable secure LDAP on Azure AD
> See the tutorial on Microsoft docs. <br>
> [https://docs.microsoft.com/zh-tw/azure/active-directory-domain-services/tutorial-create-instance](https://docs.microsoft.com/zh-tw/azure/active-directory-domain-services/tutorial-create-instance)
---
### Add Azure AD secure LDAP to openshift as an identity provider
Create the LDAP secret for use in the LDAP custom resource.

```
oc create secret generic ldap-secret --from-literal=bindPassword=pwd-of-bindDN -n openshift-config
```
Create a configmap for the LDAP server certificate.
```
oc create configmap ca-config-map --from-file=ca-for-secure-ldap=path_to_ca -n openshift-config
```
Create an ldap.yaml LDAP custom resource configuration file with the following configurations and save the file. 
```crc
apiVersion: config.openshift.io/v1
kind: OAuth
metadata:
  name: cluster
spec:
  identityProviders:
  - name: AzureAD 
    mappingMethod: claim 
    type: LDAP
    ldap:
      attributes:
        id: 
        - name
        email: 
        - mail
        name: 
        - cn
        preferredUsername: 
        - sAMAccountName
      bindDN: "CN=svc_id,OU=Users,DC=domain,DC=com" 
      bindPassword: 
        name: ldap-secret
      ca: 
        name: ca-config-map
      insecure: false 
      url: "ldaps://ldapserver.com/OU=Users,DC=domain,DC=com?sAMAccountName??(objectClass=person)"
```
<br>
Apply the LDAP custom resource configuration.

```
oc apply -f ldap.yaml
```
