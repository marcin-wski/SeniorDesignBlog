# What is PGP?
PGP stands for "Pretty Good Privacy" and has been created by Phil Zimmermann, special director of Computer Professionals for Social Responsibility (CPSR). It was meant to promote awareness of the privacy issues in the new digital age and aimed at better protecting one's privacy.

In the simplest possible words, PGP is an encryption technology, or algorithm, which helps two parties verify each other’s authenticity and helps exchange encrypted data.

# How does PGP work?

PGP makes use of two types of keys to encrypt and decrypt a text:

- The Public Key.
- The Private Key.

The public key is what’s used to encrypt the message, this key is to be shared with the person who is sending you the message so that it can be easily encrypted.

The private key, however, should be kept a secret as this key is used to decipher the received, encrypted message.

# Starting your journey

There is PLENTY of softwares for PGP encryption availabe for Windows, Linux, and Unix systems, both with GUI and terminal only, but one of the easiest GUI-based tools is [GPG4WIN](https://www.gpg4win.org/get-gpg4win.html) which you can easily and for free download and install with an easy to follow GUI interface.

Once the installation is complete you will see a Key Manager with a pop-up win shown saying "You do not have a private key yet" and prompting you to generate such key now. Then, it’ll ask you for your name, this data doesn’t need to be real, in fact, it’s better if it’s “not real”, so make sure the name you use is a fake one. Similarly, use a fake E-mail on the next screen as well. Make sure it’s “complex” and not something everyone would use such as fakeemail@email.com, instead make it something like ilovecatsandthisisafakeemail@ultrafakeemail.com

Finally, create a backup of your key. It’s not mandatory, but it could help if your primary key gets... lost.

If you do create it, it’ll ask you to “create a passphrase” in order to protect this backup key. It’s like your password, so just set something that’s hard for others to guess. It’s required while decrypting your messages.

On the next popup, select a location for your backup key. I’ll recommend using a deeper location, such as a folder inside a folder inside another folder.

Once you click on save, it’ll ask for that passphrase which you just created. This is to make sure that you’re the same person who initiated the backup key process, and that you still remember your password.

Finally, you get a confirmation, letting you know where the backup key is stored. And the program itself recommends you to store this information safely, you can either snapshot it and upload it somewhere safe, or just write the location down offline.

## Next steps after the initial setup

Now that you’ve created it, right click on the key, and select copy. This will copy your “Public key” automatically to your clipboard, which you can then send to anyone for encryption.

Or, you can manually go to the location where you backed your key up, and open it with notepad or any other text editor.

And then, copy the key from “Begin PGP Public Key Block” to “End PGP Public Key Block”.

Make sure you don’t copy the “Private keys”, and that’s the reason why the automated “copy” button from the GPG4WIN program is a much better and easier choice.

So now you have your own Public and Private keys, you can send this Public key to anyone who wishes to send you an encrypted message.

# How to use PGP to Encrypt a Message

You can encrypt both a simple text message, or whole files and folders using PGP. The Clipboard opens by default when you run the program, if it does, proceed to the next step if you’re on any other page, simply click on the “clipboard” icon from the top-bar. Type your text in the text area, and click on “Encrypt”. Then, choose the PGP public key of the person whom you wish to send this message, note that only that person will be able to decrypt this message.

Although, you can also select multiple keys, in that case, all those persons who own those keys will be able to decrypt the message.

Simply send this message to anyone you want, and only that person will be able to view this message, because it has been encrypted with their Public key.

# How to use PGP to Decrypt a Message

One of the other sides of using PGP is decrypting encrypted messages sent to you.

Before you can decrypt a message, make sure that the message has been encrypted using your PGP public key.

Once you get the encrypted message, open clipboard, paste it there and click on decrypt. It will ask you for your password; enter the password, which you setup earlier.

Once done, the message gets decrypted and copied to your clipboard, so you simply can open any text-editor like notepad, and right click > paste, or simply press ctrl+v.
