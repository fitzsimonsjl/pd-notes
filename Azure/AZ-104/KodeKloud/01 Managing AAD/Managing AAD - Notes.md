# AAD Concepts

**Identity**
- Any object that can be authenticated is considered an identity
- Can be user, group, managed identity, or service principals.

**Account**
- We associate data attributes to an identity
- User will have multiple attributes like a location, department, manager, phone no etc.

**AAD Account**
- Accounts that are created in AAD or another MS cloud service

**AAD tenant or directory**
- Dedicated instance of AAD that is created during sign up of any MS cloud service subscription
- Tenant and directory mean the same thing - can be used interchangeably
- Can have one or multiple for a company

# AAD vs AA DS

AAD and AA DS are not the same!

| AAD | AADS |
|------|-------|
| Queried using HTTP/S | Queried using LDAP |
| Protos for auth inc. SAML, WS-Fed, OID Conn, OAuth used for auth | Uses Kerberos |
| Federation can be set up with 3rd party providers | Federation is only to other domains, no 3rd party services supported |
| AAD is a managed service offering | AADS will be running on VMs or physical servers |

# AAD Editions

4 different editions (licenses):
|Features | Premium P2 | Premium P1 | M365 Apps | Free |
|---------|------------|------------|------------|-----|
| No directory object limit | Yes | Yes | Yes | No (50,000 limit) |
| SSO & Core IAM | Yes | Yes | Yes | Yes | 
| B2B Collaboration | Yes | Yes | Yes | Yes | 
| O365 Identity & Access | Yes | Yes | Yes | No |
| Hybrid Identities | Yes | Yes | No | No |
| Conditional Access | Yes | Yes | No | No |
| Identity Protection | Yes | No | No | No |
| Identity  Governance | Yes | No | No | No |

# User Accounts


