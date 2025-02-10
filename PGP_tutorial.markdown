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
</table>
</center>
