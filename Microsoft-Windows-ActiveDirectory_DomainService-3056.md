# Event Info
- Log : Security
- Source : Microsoft-Windows-ActiveDirectory_DomainService
- EventID : 3056
- Message : The directory service processed a query for the sdRightsEffective attribute on the object specified below. The returned access mask included WRITE_DAC, but only because the directory has been configured to allow implicit owner privileges which is not a secure setting. 
 
Object DN: CN=something,OU=something,OU=something,DC=something,DC=something,DC=something
 
User: DOMAIN\USER
 
Client IP Address: 1.2.3.4:56789
 
For more information, please see https://go.microsoft.com/fwlink/?linkid=2174032.

# Summary
CVE-2021-42291 addresses a security bypass vulnerability that allows certain users to set arbitrary values on security-sensitive attributes of specific objects stored in Active Directory (AD). To exploit this vulnerability, a user must have sufficient privileges to create a computer account, such as a user granted CreateChild permissions for computer objects. That user could create a computer account using a Lightweight Directory Access Protocol (LDAP) Add call that allows overly permissive access to the securityDescriptor attribute. Additionally, creators and owners can modify security-sensitive attributes after creating an account.

Mitigations in CVE-2021-42291 consist of:

Additional authorization verification when users without domain administrator rights attempt an LDAP Add operation for a computer-derived object. This includes an Audit-By-Default mode that audits when such attempts occur without interfering with the request and an Enforcement mode that blocks such attempts.

Temporary removal of the Implicit Owner privileges when users without domain administrator rights attempt an LDAP Modify operation on the securityDescriptor attribute. A verification occurs to confirm if the user would be allowed to write the security descriptor without Implicit Owner privileges. This also includes an Audit-By-Default mode that audits when such attempts occur without interfering with the request and an Enforcement mode that blocks such attempts.

# Notes
Enforcement mode will be turned on by default in an upcoming update no sooner than January 9, 2024.

# Links
[KB5008383—Active Directory permissions updates (CVE-2021-42291)] ( https://prod.support.services.microsoft.com/en-us/topic/kb5008383-active-directory-permissions-updates-cve-2021-42291-536d5555-ffba-4248-a60e-d6cbc849cde1 )
