---
title: Setting up and using PGP
author: nedwards
layout: post
categories:
  - backup
  - Bash
  - Linux
---
During the course of my work, I have needed to setup gnupg for exchanging and protecting sensitive information. On a standard Ubuntu install this should be already installed. As an aside a good Linux GUI for this is [Seahorse][1]

Firstly generate and new key pair. Just accept the defaults and use your email address as the id.  
`<br />
gpg &#45;&#45;gen-key<br />
`

Now check your new key is listed.  
`gpg &#45;&#45;list-keys`

Export your public key  
`gpg &#45;&#45;export --armor myname@domain.com  > my_public_key`

Now that you have your public key your can send it to anyone and they can then encrypt files with it and then only you can decrypt with your private key.  
*The &#45;&#45;armour option above ensures that the key is exported as ascii and not binary*

Import public key  
`gpg --import public.key`

Sign key  
`gpg --sign-key otheruser@domain.com`

You can now encrypt a file that can only be decrypted by the owner of the public key with (you would have received a warning if you had not signed the imported key)  
`gpg -r otheruser@domain.com -e file`

#### Integrating with logrotate

The idea here is to use pgp to encrypt certain sensitive log files on a server, using a gpg public key. The way that logrotate will work will be the same, however no one will be able to view the encrypted logfile without the relevant private key.

Firstly we need to import the public key that we have created previously, I am assuming here that we are on an external server that only has the public key present:

`<br />
gpg &#45;&#45;import my_public_key<br />
`

Now trust the public key:

`<br />
gpg &#45;&#45;edit-key user-id<br />
trust<br />
quit<br />
`

Firstly we need the long key id:

`<br />
gpg &#45;&#45;list-keys &#45;&#45;with-colon user@domain.com<br />
`  
The long key id is in the fifth column starting on the line starting with pub.

Now we can encrypt a file with a command like the following:

`<br />
cd /var/log/apache2<br />
gpg &#45;&#45;trusted-key <long_key_id> -r user@domain.com -e audit.log</p>
<p>`

##### Modify logrotate

Modify the /etc/logrotate.d/apache2 file to include the following:

`<br />
/var/log/apache2/audit.log {<br />
	daily<br />
	missingok<br />
	delaycompress<br />
	compress<br />
	compresscmd /usr/local/lib/gpg_logs<br />
	compressext .pgp<br />
	rotate 365<br />
	notifempty<br />
	create 640 root adm<br />
	sharedscripts<br />
	postrotate<br />
		if [ -f /var/run/apache2.pid ]; then<br />
			/etc/init.d/apache2 restart > /dev/null<br />
		fi<br />
	endscript<br />
}<br />
`

The compresscmd script /usr/local/lib/gpg_logs just contains the following, please create:

`<br />
#!/bin/bash</p>
<p>/usr/bin/gpg &#45;&#45;trusted-key <long_key_id> &#45;&#45;trusted-key <long_key_id> &#45;&#45;trusted-key <long_key_id> -r user1@domain.com -r user2@domain.com -r user3@domain.com -e $1<br />
returnvalue=$?</p>
<p>if [ $returnvalue -eq 0 ] ;<br />
then<br />
# don't delete until sure this is working reliably<br />
rm -f $1<br />
fi<br />
`

The above gpg command encrypts files using three different pgp keys. So in effect this means that the file can be decrypted using any of the corresponding private keys.

Now ensure that the script can be run:  
`<br />
chmod u+x /usr/local/bin/gpg_logs<br />
`

 [1]: http://www.gnome.org/projects/seahorse
