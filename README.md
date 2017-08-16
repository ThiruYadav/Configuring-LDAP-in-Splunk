# Configuring-LDAP-in-Splunk
LDAP Configuration in Splunk

Prerequisites for LDAP authentication:
I) Active Directory domain is set up
II) created records in DNS for ldap.example.com.
III) An Enterprise CA in our Active Directory, and all our domain controllers have certificates

configuration:
logon to Splunk and then select the Manager link in the upper right and then click on authentication method
Click on radio button in front of LDAP and then click “Configure Splunk to work with LDAP
3. Now you will get  main LDAP strategy configuration settings page. Following are the main AD items that you need to enter here –

a. LDAP connection settings – based on connection settings Splunk will talk to AD.

LDAP strategy name: just a name.

You can have multiple LDAP strategies such as –  (i)strategy one for ready only access through an AD Group mapping to Splunk roles (user & power user), (ii)strategy two for full access through another AD Group mapping to other Splunk roles (Admin, Splunk-system-role) or similar.

Default Splunk roles are – admin, can_delete, power, splunk-system-role, user.

Port number: 389 (this is AD LDAP default)

Connection order: default

Bind DN: cn= AcctName Splunk,ou=yourSvcAcctOU,dc=yourDCName,dc=yourDCExtension

This is distinguished name of your Splunk account that you created in AD. It is recommended you should not use default AD administrator account or your own AD login here. You should create a dedicate account for Splunk – no AD administrative privilege required on this account.

Bind DN Password: enter the password of AD Splunk account
b. User Settings – Splunk will look for users in AD based on this

User base DN: dc=yourDCName,dc=yourDCextension

User base filter: leave this blank or you can enter specific AD search filter here

User name attribute: samaccountname

Real name attribute: displayname

Group mapping attribute: dn
c. Group settings – Splunk will look for AD groups in AD based on this

Group base DN: cn=Group_Splunk_Access_Admins,ou=youGroupOUName,dc=yourDCName,dc=DCextension

This is the AD group that been created to grant access in Splunk.
d. Dynamic group settings – optional

e. Advanced settings – default is ok; however you can increase search request size limit.
1.     Click on the “Save”. If entered parameters are not correct – you won’t be able to save.

2.     Now you should be able to see your LDAP strategy. Make sure it is enabled.

3.     To see your AD group in Splunk, click on “Map groups”.

Also you should be able to see AD users at “Settings > Access controls >Users”. Make sure AD users are member of the Splunk group that been created on AD.

 -  That’s all Your AD authentication is ready now and users from AD whose group mapped in splunk can login to splunk.


