# Mail Server

Unix-based mail servers are built using a number of components because a Unix-style environment is, by default, a toolbox operating system. A stock Unix-like server already has internal mail, more traditional ones also come with a full MTA (Mail Transfer Agent) already part of the standard installation. To allow the server to send external emails, an MTA such as Sendmail, Postfix, or Exim is required. Mail is read either through direct access (shell login) or mailbox protocols like POP and IMAP. Unix based MTA software largely acts as enhancement or replacement of the respective system's "native" MTA.

Windows servers do not natively implement email. Windows-based MTAs therefore have to cover the whole set of email-related functionality. 

# Setting up Postifx on Ubuntu Server

## SSL Certificate

For SSL Certificate for your mail server, you'll need a certificate and a private key. The certificate is generally saved in `/etc/ssl/certs/mailcert.pem` and the key in `/etc/ssl/private/mail.key`.

First let's create a self-signed test certificate:
`sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/mail.key -out /etc/ssl/certs/mailcert.pem`

Let's follow this up with a Certificate Signing Request (CSR):
`sudo openssl req -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/mail.key -out mailcert.csr`

## DNS

Like with any web server, you want to be able to have an FDQN - Fully Qualified Domain Name with an actual domain, so that your emails can be sent and received properly and without additional issues.

## Postfix

Let's first update your system, just to be sure, and then install Postfix:
`sudo apt-get update`
`sudo DEBIAN_PRIORITY=low apt-get install postfix`

Now you'll be guided through a series of questions, please see the general guide below if you're having any issues with answering them at the moment:

- General type of mail configuration?: Internet Site
- System mail name: trustytruck.com (not mail.example.com)
- Root and postmaster mail recipient: root
- Other destinations to accept mail for: $myhostname, example.com, mail.example.com, localhost.example.com, localhost
- Force synchronous updates on mail queue?: No
- Local networks: 127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128
- Mailbox size limit: 0
- Local address extension character: +
- Internet protocols to use: all

If you need to at any time come back and re-adjust these settings (perhaps because your domain has changed) you can easily do so with `sudo dpkg-reconfigure postfix`

### Configure Postfix

Let's first set the home_mailbox variable to Maildir/ which will create a directory structure under that name within the user’s home directory. The postconf command can be used to query or set configuration settings. Configure home_mailbox by typing:
`sudo postconf -e 'home_mailbox= Maildir/'`

Now we will set the location of the virtual_alias_maps table. This table maps arbitrary email accounts to Linux system accounts. We will create this table at /etc/postfix/virtual. Again, we can use the postconf command:
`sudo postconf -e 'virtual_alias_maps= hash:/etc/postfix/virtual'`

In `/etc/postfix/virtual` will have to set up virtual maps file and make sure the emails are sent with correct information:
contact@<your domain>.com root
admin@<your domain>.com root

Let's go now set up the environmental variables for our MAIL:
`echo 'export MAIL=~/Maildir' | sudo tee -a /etc/bash.bashrc | sudo tee -a /etc/profile.d/mail.sh`

In order to interact with the mail being delivered, we will install the s-nail package. This is a variant of the BSD xmail client which is feature-rich, can handle the Maildir format correctly, and is mostly backwards compatible. To install the s-nail package simply type:
`sudo apt-get install s-nail`

In `/etc/s-nail.rc` we'll now add these options on the bottom, which will allow the client to open even with an empty inbox. It will also set the Maildir directory to the internal folder variable and then use this to create a sent mbox file within that, for storing sent mail:
`set emptystart
set folder=Maildir
set record=+sent`
