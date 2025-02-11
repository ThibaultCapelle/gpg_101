---
layout: post
title:  "PGP beginner tutorial"
date:   2025-02-08 19:50:01 +0100
categories: jekyll update
numbersections: true
---

Here is a small tutorial for getting started with this protocol named Pretty Goog Privacy (PGP), an assymetric cryptographic tool that allows to have end to end encrypted mails despite using very mainstream services like gmail, outlook, etc. You will find several names around, like GPG, PGP, OpenPGP. I will use them interchangeably as they basically refer to the same thing.


<div class="warning" style='padding:0.1em; background-color:#E9D8FD; color:#69337A'>
<span>
<p style='margin-top:1em; text-align:center'>
<b>end to end encrypted</b></p>
<p style='margin-left:1em;'>
<b>end to end encryption</b> means that you communicate with someone in the following way:
<ol>
<li>you encrypt the message on your local machine (phone or laptop for example)</li>
<li>you send it to a server (for example Gmail, discord, a SMS service, etc.) that will send it to the person you want to communicate with.</li>
<li>the person you want to communicate to decrypt the message on their local machine</li>
</ol>
Doing this allows to use a server that you do not trust without risking the information you send to be seen by anyone who administrate this server

</p>
</span>
</div>

The principle is the following: each user generates a pair of key:
1. A private key, that they will keep for themselves and share with ***NO ONE ELSE***. This is used to ***decrypt*** files
2. A public key, that they will share to the people they want to communicate to. This is used to ***encrypt*** files.

The keys have the following properties:
1. you can generate the public key from the private one very easily
2. you cannot generate the private key knowing the public key

<div class="hello" style='padding:0.1em; background-color:#E9D8FD; color:#69337A'>
<span>
<p style='margin-top:1em; text-align:center'>
<b>Limitations of the protocol</b></p>
<p style='margin-left:1em;'>
Encrypting the content of the message does not mean that you hide everything. In principle, for a mail encrypted with PGP, the following informations are still unencrypted:
<ul>
<li>The "From" and "To" field</li>
<li>the subject of the mail (try to use vague subjects or no subject at all)</li>
<li>the server knows at least which IP address is contacting them, and which account they host is used</li>
</ul>
</p>
</span>
</div>


### Sending end to end encrypted mails

Let us start straigtaway with a common usecase of this tool: you want to send a mail to someone without your mail server to know about its content.

# Using a web client, instead of a web server

The first thing you want to do is to set up a web client if you have not done it. Whatever your platform is, you can use
[Mozilla Thunderbird](https://www.thunderbird.net/en-US/), which is open source, free and includes PGP, with a key manager, by default.
Alternatively, if you are using Windows and Microsoft Outlook, you can install a free an open source gpg plugin called [GPG4Win](https://www.gpg4win.org/). This will add a plugin to Outlook to use PGP, install a key manager called Kleopatra, and install the gpg command line tool.
For MacOs, there exists a software called [GPGTools](https://gpgtools.org/) that you can download, but it is not free (it costs 24 euros). So I would suggest you then use Thunderbird and (although not usually necessary for all applications) the command line tool that you can install using Homebrew with the command:

```console
foo@bar:~$ brew install gnupg
```
<div class="hello" style='padding:0.1em; background-color:#E9D8FD; color:#69337A'>
<span>
<p style='margin-left:1em;'>
Before, you might need to install Homebrew, if you have not already, entering this command in a terminal:
<pre><samp>
foo@bar:~$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
</samp></pre>
</p>
</span>
</div>

Once you have a functional web client, the various way of setting up PGP are now going to be decribed:

## Windows with Microsoft Outlook and GNU4Win

Start by downloading it:
<center>
<table>
    <tr><img src="assets/img/gpg4win.png" alt="drawing" width="800"/>
    Clik on download, and you can choose how much you would like to donate, including 0$, then install the program with the default options
    </tr>
    <tr><img src="assets/img/gpg4win_2.png" alt="drawing" width="800"/></tr>
    <tr><img src="assets/img/gpg4win_3.png" alt="drawing" width="800"/></tr>
</table>
</center>
This will open the PGP key manager Kleopatra.
<center>
<table>
    <tr><img src="assets/img/kleopatra_1.png" alt="drawing" width="800"/><br>
    Click on "New key pair"<br>
    </tr>
    <tr><img src="assets/img/keypair_generation.png" alt="drawing" width="400"/><br>
    Enter a name and your email, then tick the "passphrase" option
    </tr>
    <tr><img src="assets/img/kleopatra_2.png" alt="drawing" width="800"/>
    </tr>
    <tr><img src="assets/img/kleopatra_3.png" alt="drawing" width="800"/><br>
    Click on "Settings"
    </tr>
    <tr><img src="assets/img/kleopatra_4.png" alt="drawing" width="800"/><br>
    Then on "Configure Kleopatra"
    </tr>
    <tr><img src="assets/img/kleopatra_5.png" alt="drawing" width="800"/><br>
    Set the keyserver "hkps://keys.openpgp.org", then click on "OK"
    </tr>
    <tr><img src="assets/img/kleopatra_6.png" alt="drawing" width="400"/><br>
    Right click on your key and click on "Publish on Server" if you want anyone to find your public key, or alternatively export it to a file to give it only to a selected few people.
    </tr>
    <tr><img src="assets/img/kleopatra_7.png" alt="drawing" width="800"/><br>
    Click on "Lookup on server" to find keys uploaded on public servers. In the search field enter the full mail address of the person you are looking for<br>
    </tr>
    <tr><img src="assets/img/kleopatra_8.png" alt="drawing" width="400"/><br>
    After importing the key, certify it by right click->certify. Verify the fingerprint with the person you are talking to, either physically or with secure channels, for example using Signal.
    </tr>
    <tr><img src="assets/img/kleopatra_10.png" alt="drawing" width="800"/><br>
    Open a new mail, and write the mail address of the person you want to write to in the "To" field. Click on the GpgOL option "Secure" and you should see the two options "Sign" and "Encrypt" squared in black, meaning that they are activated. Write your mail (remember to use a vague subject or no subect at all) and then hit "send". That's it ! You can then check on your webmail to see what the server actually receives, which should be only encrypted data. Attachements are also encrypted, if you used any.
    </tr>
</table>
</center>

## All platforms with Mozilla Thunderbird

Once you have a set up thunderbird installation with your mail server, open it and do the following:

<center>
<table>
    <tr><img src="assets/img/thunderbird_2.png" alt="drawing" width="250"/><br>
    Right click on your mail address on the left, then click on "Settings" <br>
    </tr>
    <tr><img src="assets/img/thunderbird_3.png" alt="drawing" width="800"/><br>
    In the "End to End encryption" section, click on "OpenPGP Key Manager"
    </tr>
    <tr><img src="assets/img/thunderbird_4.png" alt="drawing" width="400"/>
    Click on Generate->New Key Pair
    </tr>
    <tr><img src="assets/img/thunderbird_5.png" alt="drawing" width="400"/><br>
    After the key generation, click on Keyserver->Publish if you want anyone to be able to find your public key. Then you can find enother person public key with Keyserver-Discover Keys Online. Remember to enter the full mail address associated with the key you are looking for in the search field. Alternatively, you can use File->Import Public Key from File and File->Export Public Key to File functions to share your public key to a smaller audience.
    </tr>
    <tr><img src="assets/img/thunderbird_6.png" alt="drawing" width="800"/><br>
    Go back to Settings, then select your key as the default key for your mail address
    </tr>
    <tr><img src="assets/img/thunderbird_7.png" alt="drawing" width="800"/><br>
    Open a new mail, and write the mail address of the person you want to write to in the "To" field. You should see appearing the mention "OpenPGP end-to-end-encryption is possible", and you can then click on "Encrypt". You can also click on the Encrypt button next to send to have the same effect. Write your mail (remember to use a vague subject or no subect at all) and then hit "send". That's it ! You can then check on your webmail to see what the server actually receives, which should be only encrypted data. Attachements are also encrypted, if you used any.
    </tr>
    <tr><img src="assets/img/thunderbird_8.png" alt="drawing" width="400"/><br>
    We need now to activate a master password to encrypt the keys (and also the mails on your computer at rest) by going to Settings->Thunderbird Settings
    </tr>
    <tr><img src="assets/img/thunderbird_9.png" alt="drawing" width="800"/><br>
    Then click on "Privacy and Security"->"Use a primary password" and set up a strong passphrase<br>
    </tr>
</table>
</center>

### Encrypting and decrypting files with GPG, regardless of the fact that you use email to transfer them

## Using Windows and GNU4Win

If you are on Windows and have installed GNU4WIN (see above), then you can simply open the file explorer, right click on a file and see the options "sign and encrypt" and "More GpgEx options" to generate an encrypted file with a public key you previously stored with Kleopatra, or to decrypt it with your private key.

<img src="assets/img/gpgol_encrypt.png" alt="drawing" width="350"/>

## On all platforms using the command line tool gpg

This command line tool is already installed natively in basically every Linux distribution, and is installed on Windows with the installation of Gnu4Win. On MacOS, it can be installed with homebrew (see above). You can use it to bypass any of the mail system assumption, and therefore transfer things via not only any mail systems, but also other messaging apps, while being certain that it is end to end encrypted.

Here is a cheat sheet for the commands you can enter with it:

| Function     | Command      | Note|
| generate a public/private key pair | ```gpg full-generate-key``` | |
| list all public keys | ```gpg --list-keys``` | you can see the signature of the key, the level of trust under brackets, the validity f the key, and the name and mail addresses|
| list all private keys | ```gpg --list-secret-keys``` | you can see the signature of the key, the level of trust under brackets, the validity f the key, and the name and mail addresses|
| send a key to a keyserver | ```gpg --send-keys [key_id]``` | replace ```[key_id]``` with the fingerprint of the key you want to send. Default to keys.openpgp.org, but this can be changed with the --keyserver option|
| get the fingerprint of a key | ```gpg --fingerprint [mail]``` | replace ```[mail]``` with the mail address of the key you want to investigate |
| search for a public key on a server | ```gpg --search-keys [mail]``` | replace ```[mail]``` with the mail address of the person you want to communicate to. It will return the fingerprint of the found key(s) |
| Receive a key from a keyserver | ```gpg --receive-keys [key_id]``` | replace ```[key_id]``` with the fingerprint of the key you want to receive, that you would tipycally have found with the ```gpg --search-keys [mail]```command above |
| Import a public key from a file | ```gpg --import [key_file]``` | replace ```[key_file]``` with the file containing the public key you want to import in your keyring |
| Export a public key to a file | ```gpg --export [mail] > [filename]``` | replace ```[mail]``` with the mail of the key you want to export, and ```[filename]``` by the name of the file you want to create|
| Encrypt a file with GPG | ```gpg --encrypt --recipient [mail] --sign --armor [filename]``` | replace ```[mail]``` with the mail of a person you have the public key of, and ```[filename]``` with the file you want to encrypt. This will create another file named ```filename.asc```which is a text file containing the encrypted data.|
| Decrypt a file with GPG | ```gpg [filename]``` | replace ```[filename]``` with the file you want to decrypt. This will create another file that is the decrypted file. If you want to specify the name of the output file, you can use the option ```--output [filename]```|


### Signing and verifying signatures with OpenPGP

PGP is not only used to encrypt, but also to make "signatures" and to verify them, to check that:
1. the sender of the message is the person you think they are, or
2. that the file you downloaded has not been tampered with while being sent to you

The signature mechanism works in the opposite way as the encryption:
1. Your ***private key*** is used to ***sign***
2. Your ***public key*** is used by the person receiving the message to ***verify the signature***

The way it is done is the following:
1. The file is ***hashed*** (see the paragraph below).
2. This hashed file is encrypted with your private key
3. The result is added at the end of your file, giving a ***signed*** file.

<div class="warning" style='padding:0.1em; background-color:#E9D8FD; color:#69337A'>
<span>
<p style='margin-top:1em; text-align:center'>
<b>Hash function</b></p>
<p style='margin-left:1em;'>
<b>to hash</b> means applying a <b>hash function</b>. A hash function is a complicated function that:
<ol>
<li>for any file or string input returns a string of a fixed size</li>
<li>is injective (two different inputs give two different output)</li>
<li>is very hard to invert (two inputs that are different by only one character will give two very different outputs)</li>
</ol>
</p>
</span>
</div>

Actually, in most case you will do both: signing (with your private key) then encrypting (with the public key of someone else). The person receiving the message will decrypt it with their private key, and then extract the signature and verify it with your public key.

## Checking the integrity of a downloaded file

In some case you will download something from a website and there will be a signature associated with it, like in this example from the software [veracrypt](https://www.veracrypt.fr/en/Downloads.html):

<img src="assets/img/signature_file_example_veracrypt.png" alt="drawing" width="800"/>

You can download the file, the associated signature and the public key. In the veracrypt example, the public key can be found [here](https://www.idrix.fr/VeraCrypt/VeraCrypt_PGP_public_key.asc). You can import it with:

```console
wget https://www.idrix.fr/VeraCrypt/VeraCrypt_PGP_public_key.asc && gpg --import VeraCrypt_PGP_public_key.asc
```

In the download page, they tell you to check that the fingerprint is correct:

```console
foo@bar:~ gpg --fingerprint veracrypt@idrix.fr
pub   rsa4096 2018-09-11 [SC]
      5069 A233 D55A 0EEB 174A  5FC3 821A CD02 680D 16DE
uid           [ unknown] VeraCrypt Team (2018 - Supersedes Key ID=0x54DDD393) <veracrypt@idrix.fr>
sub   rsa4096 2018-09-11 [E]
sub   rsa4096 2018-09-11 [A]
```

and that it should be 5069 A233 D55A 0EEB 174A 5FC3 821A CD02 680D 16DE.
Once you checked the fingerprint the public key, you can sign it with your private key to indicate that you trust it:

```console
foo@bar:~ gpg --sign-key veracrypt@idrix.fr
pub  rsa4096/821ACD02680D16DE
     created: 2018-09-11  expires: never       usage: SC
     trust: unknown       validity: unknown
sub  rsa4096/200B5A9D26878A32
     created: 2018-09-11  expires: never       usage: E
sub  rsa4096/0F5AACD65483D029
     created: 2018-09-11  expires: never       usage: A
[ unknown] (1). VeraCrypt Team (2018 - Supersedes Key ID=0x54DDD393) <veracrypt@idrix.fr>


pub  rsa4096/821ACD02680D16DE
     created: 2018-09-11  expires: never       usage: SC
     trust: unknown       validity: unknown
 Primary key fingerprint: 5069 A233 D55A 0EEB 174A  5FC3 821A CD02 680D 16DE

     VeraCrypt Team (2018 - Supersedes Key ID=0x54DDD393) <veracrypt@idrix.fr>

Are you sure that you want to sign this key with your
key "my Name <my@mail.net>" (my_key_id)

Really sign? (y/N) y
```

you can then check that you have the correct file by entering:

```console
foo@bar:~ gpg --verify "VeraCrypt Setup 1.26.20.exe.sig" "VeraCrypt Setup 1.26.20.exe"
gpg: Signature made Tue 04 Feb 2025 15:53:43 CET
gpg:                using RSA key 5069A233D55A0EEB174A5FC3821ACD02680D16DE
gpg: checking the trustdb
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: depth: 0  valid:   3  signed:   1  trust: 0-, 0q, 0n, 0m, 0f, 3u
gpg: depth: 1  valid:   1  signed:   0  trust: 1-, 0q, 0n, 0m, 0f, 0u
gpg: next trustdb check due at 2025-11-29
gpg: Good signature from "VeraCrypt Team (2018 - Supersedes Key ID=0x54DDD393) <veracrypt@idrix.fr>" [full]
```

This Good signature indication tells you that you have downloaded a file that was certified as genuine by the owner of the private key associated with veracrypt, and that it has not been tampered with.

## Signing a document

With the command line, you can sign a document with ```gpg --sign [filename]``` to output a signed document or ```gpg --detach-sign [filename]``` to output only the signature.

## Sign the public key of someone

GPG is a lot based on the trust that you are talking to the right person. Therefore, to tell to the whole world that you trust some public key, you should ***sign the public keys*** of other people.

This is how to do it (as recommended [here](https://gist.github.com/F21/b0e8c62c49dfab267ff1d0c6af39ab84)):

1. Alice (you) get the public key of Bob
2. Alice sign it with her private key: ```gpg --sign-key [key_id]``` where ```[key_id]``` is the fingereprint of the Bob public key. In the process you will be asked to check that the fingerprint match with the key of the other person, which you should do in a secure channel, or in person, with the person owning the key.
3. Alice exports, then encrypts the signed key with Bob public key, with the following command: ```gpg --armor --export [key_id] | gpg --sign --encrypt -r [key_id] > [filename]```, where ```[key_id]```is the fingereprint of Bob public key and ```[filename]```is the output filename
4. Alice email the key to Bob using the mail adress associated with the key
5. Bob receives it, then decrypt it with his private key and import it: ```gpg --decrypt [filename]``` and then ```gpg --import [filename_decrypted]```
6. He can then send it to a keyserver, containing Alice signature: ```gpg --send_keys [key_id]```


