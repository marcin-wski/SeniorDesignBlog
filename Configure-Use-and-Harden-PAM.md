# What is PAM

Linux-PAM (short for Pluggable Authentication Modules which evolved from the Unix-PAM architecture) is a powerful suite of shared libraries used to dynamically authenticate a user to applications (or services) in a Linux system.

It integrates multiple low-level authentication modules into a high-level API that provides dynamic authentication support for applications. This allows developers to write applications that require authentication, independently of the underlying authentication system.

To employ PAM, an application/program needs to be “PAM aware“ which means it needs to be written and compiled specifically to use PAM. You can check whether the application has been made “PAM-aware” simply by using the ldd command, like he for the SSH service:

`sudo ldd /usr/sbin/sshd | grep libpam.so`

# Configuring PAM

The main configuration file for PAM is /etc/pam.conf and the /etc/pam.d/ directory contains the PAM configuration files for each PAM-aware application/services. PAM will ignore the file if the directory exists. Each file in this directory has the same name as the service to which it controls access. For example, the "login" program defines its service name as login and installs the /etc/pam.d/login PAM configuration file.

Red Hat recommends to configure PAM using the "autoconfig" tool, however, it is also easy to update the configuration manually.

## Configuration file format

Each PAM configuration file contains a group of directives that define the module (the authentication configuration area) and any controls or arguments with it. The directives all have a simple syntax that identifies the module purpose (interface) and the configuration settings for the module.

The directives all have a simple syntax that identifies the module purpose (interface) and the configuration settings for the module. The format of each rule is a space separated collection of tokens (the first three are case-insensitive)

`service type control-flag module module-arguments`

where:

- service: actual application name.
- type: module type/context/interface.
- control-flag: indicates the behavior of the PAM-API should the module fail to succeed in its authentication task.
- module: the absolute filename or relative pathname of the PAM.
- module-arguments: space separated list of tokens for controlling module behavior.

In a PAM configuration file, the module interface is the first field defined. For example:

`auth	required	pam_unix.so`

This instructs PAM to use the pam_unix.so module's auth interface. Module interface directives can be stacked, or placed upon one another, so that multiple modules are used together for one purpose. If a module's control flag uses the sufficient or requisite value, then the order in which the modules are listed is important to the authentication process. 

# Groups and Control-flags

PAM authentication tasks are separated into four independent management groups. These groups manage different aspects of a typical user’s request for a restricted service.

A module is associated to one these management group types:

- account: provide services for account verification: has the user’s password expired?; is this user permitted access to the requested service?.
- authentication: authenticate a user and set up user credentials.
- password: are responsible for updating user passwords and work together with authentication modules.
- session: manage actions performed at the beginning of a session and end of a session.

PAM loadable object files (the modules) are to be located in the following directory: /lib/security/ or /lib64/security depending on the architecture.

The supported control-flags are:

- requisite: The module result must be successful for authentication to continue. However, if a test fails at this point, the user is notified immediately with a message reflecting the first failed required or requisite module test.
- required: The module result must be successful for authentication to continue. If the test fails at this point, the user is not notified until the results of all module tests that reference that interface are complete. 
- sufficient: The module result is ignored if it fails. However, if the result of a module flagged sufficient is successful and no previous modules flagged required have failed, then no other results are required and the user is authenticated to the service. 
- optional: The module result is ignored. A module flagged as optional only becomes necessary for successful authentication when no other modules reference the interface. 

In addition to the above are the keywords, there are two other valid control flags:

- include: include all lines of given type from the configuration file specified as an argument to this control.
- substack: include all lines of given type from the configuration file specified as an argument to this control.

# Restrict root access to SSH

You'll have add this rule to both `/etc/pam.d/sshd` and `/etc/pam.d/login`:

`auth    required       pam_listfile.so       onerr=succeed  item=user  sense=deny  file=/etc/ssh/deniedusers`

Next, we need to create the file /etc/ssh/deniedusers and add the name root in it `etc/ssh/deniedusers`. From now on, the above rule will tell PAM to consult the /etc/ssh/deniedusers file and deny access to the SSH and login services for any listed user.
