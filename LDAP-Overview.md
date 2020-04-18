# What is LDAP

The Lightweight Directory Access Protocol - LDAP - is an open, vendor-neutral, industry standard application protocol for accessing and maintaining distributed directory information services over an Internet Protocol (IP) network. Directory services play an important role in developing intranet and Internet applications by allowing the sharing of information about users, systems, networks, services, and applications throughout the network. As examples, directory services may provide any organized set of records, often with a hierarchical structure, such as a corporate email directory. Similarly, a telephone directory is a list of subscribers with an address and a phone number.

# LDAP Overview

A client starts an LDAP session by connecting to an LDAP server, called a Directory System Agent (DSA), by default on TCP and UDP port 389, or on port 636 for LDAPS. The client then sends an operation request to the server, and a server sends responses in return. With some exceptions, the client does not need to wait for a response before sending the next request, and the server may send the responses in any order. All information is transmitted using Basic Encoding Rules - BER.

The client may request the following operations:

- StartTLS – use the LDAPv3 Transport Layer Security (TLS) extension for a secure connection
- Bind – authenticate and specify LDAP protocol version
- Search – search for and/or retrieve directory entries
- Compare – test if a named entry contains a given attribute value
- Add a new entry
- Delete an entry
- Modify an entry
- Modify Distinguished Name (DN) – move or rename an entry
- Abandon – abort a previous request
- Extended Operation – generic operation used to define other operations
- Unbind – close the connection (not the inverse of Bind)

In addition the server may send "Unsolicited Notifications" that are not responses to any request, e.g. before the connection is timed out.

A common alternative method of securing LDAP communication is using an SSL tunnel. The default port for LDAP over SSL is 636. The use of LDAP over SSL was common in LDAP Version 2 (LDAPv2) but it was never standardized in any formal specification. This usage has been deprecated along with LDAPv2, which was officially retired in 2003. Global Catalog is available by default on ports 3268, and 3269 for LDAPS

# Structure of the directory

The protocol provides an interface with directories that follow the 1993 edition of the X.500 model:

- An entry consists of a set of attributes.
- An attribute has a name (an attribute type or attribute description) and one or more values. The attributes are defined in a schema (see below).
- Each entry has a unique identifier: its Distinguished Name (DN). This consists of its Relative Distinguished Name (RDN), constructed from some attribute(s) in the entry, followed by the parent entry's DN. Think of the DN as the full file path and the RDN as its relative filename in its parent folder (e.g. if /foo/bar/myfile.txt were the DN, then myfile.txt would be the RDN).

# Two implementations:

## OpenLDAP

OpenLDAP is a free, open-source implementation of the Lightweight Directory Access Protocol (LDAP) developed by the OpenLDAP Project. It is released under its own BSD-style license called the OpenLDAP Public License.

LDAP is a platform-independent protocol. Several common Linux distributions include OpenLDAP Software for LDAP support. The software also runs on BSD-variants, as well as AIX, Android, HP-UX, macOS, Solaris, Microsoft Windows (NT and derivatives, e.g. 2000, XP, Vista, Windows 7, etc.), and z/OS. 

### OpenLDAP Components

OpenLDAP has three main components:

- slapd – stand-alone LDAP daemon and associated modules and tools
- libraries implementing the LDAP protocol and ASN.1 Basic Encoding Rules (BER)
- client software: ldapsearch, ldapadd, ldapdelete, and others

Additionally, the OpenLDAP Project is home to a number of subprojects:

- JLDAP – LDAP class libraries for Java
- JDBC-LDAP – Java JDBC - LDAP Bridge driver
- ldapc++ – LDAP class libraries for C++
- Fortress - Role-based identity access management Java SDK
- LMDB - Memory-mapped database library

## Active Directory

Active Directory (AD) is a directory service developed by Microsoft for Windows domain networks. It is included in most Windows Server operating systems as a set of processes and services. Initially, Active Directory was only in charge of centralized domain management. Starting with Windows Server 2008. However, Active Directory became an umbrella title for a broad range of directory-based identity-related services.

A server running Active Directory Domain Service (AD DS) is called a domain controller. It authenticates and authorizes all users and computers in a Windows domain type network—assigning and enforcing security policies for all computers and installing or updating software. For example, when a user logs into a computer that is part of a Windows domain, Active Directory checks the submitted password and determines whether the user is a system administrator or normal user. Also, it allows management and storage of information, provides authentication and authorization mechanisms, and establishes a framework to deploy other related services: Certificate Services, Active Directory Federation Services, Lightweight Directory Services, and Rights Management Services.

Active Directory uses Lightweight Directory Access Protocol (LDAP) versions 2 and 3, Microsoft's version of Kerberos, and DNS.

## What are the differences between LDAP and Active Directory?

Lightweight Directory Access Protocol or LDAP, is a standards based specification for interacting with directory data. Directory Services can implement support of LDAP to provide interoperability among 3rd party applications.

Active Directory is Microsoft's implementation of a directory service that, among other protocols, supports LDAP to query it's data.

While it supports LDAP, Active Directory provides a host of extensions and conveniences, such as password expiration and account lockout.
