# Red Hat Enterprise Linux Identity Management

The RHEL Identity Management (sometimes shortened to just IdM) is a way to create identity stores, centralized authentication, domain control for Kerberos and DNS services, and authorization policies — all on Linux systems, using native Linux tools. While centralized identity/policy/authorization software is hardly new, Identity Management is one of the only options that supports Linux/Unix domains. It provides a unifying skin for standards-defined, common network services, including PAM, LDAP, Kerberos, DNS, NTP, and certificate services, and it allows Red Hat Enterprise Linux systems to serve as the domain controllers.

IdM does three things:

- Create a Linux-based and Linux-controlled domain. Both IdM servers and IdM clients are Linux or Unix machines. While IdM can synchronize data with an Active Directory domain to allow integration with Windows servers, it is not an administrative tool for Windows machines and it does not support Windows clients. Identity Management is a management tool for Linux domains.
- Centralize identity management and identity policies.
- Build on existing, native Linux applications and protocols. While IdM has its own processes and configuration, its underlying technologies are familiar and trusted by Linux administrators and are well established on Linux systems. 

# IdM vs LDAP

At the most basic level, Red Hat Identity Management is a domain controller for Linux and Unix machines. Identity Management defines the domain, using controlling servers and enrolled client machines. This provides centralized structure that has previously been unavailable to Linux/Unix environments, and it does it using native Linux applications and protocols.

The primary feature of an LDAP directory is its generality. It can be made to fit into a variety of applications. Identity Management, on the other hand, has a very specific purpose and fits a very specific application. It focuses on identities (user and machine) and policies that relate to those identities and their interactions. While it uses an LDAP backend to store its data, IdM has a highly-customized and specific set of schema that defines a particular set of identity-related entries and defines them in detail.

LDAP directories have flexibility and adaptability which makes them a perfect backend to any number of applications and its primary purpose is to store and retrieve data in the most efficient way possible. IdM fills a very different niche. It is optimized to perform a single task very effectively. It stores user information and authentication and authorization policies, as well as other information related to access, like host information. Its single purpose is to manage identities. 

# Is it possible to migrate from LDAP to Identity Management

When an infrastructure has previously deployed an LDAP server for authentication and identity lookups, it is possible to migrate the user data, including passwords, to a new Identity Management instance, without losing user or password data.
Identity Management even has specific migration tools to help move directory data and streamline the whole process for the administrators.
