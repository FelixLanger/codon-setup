# SSH Setup


### Requirements

- **A working operating system.**
- **Your EBI registered laptop or workstation.** If you have a personal laptop not registered by the EBI Systems IT team, this setup will not work.
- **Connection to the EBI internal network.** This means connection throught the EBI wired network through an ethernet cable or connection to the EBI wireless network through thr "EBI" wifi. Please check you are not connected to "eduroam", as this is a common source of problems.
- **Your smartphone with a Google Authenticator compliant application.** More details below, but you need your smartphone at hand.


### 1) The SSH config file

Check the SSH version of your local machine:

```bash
ssh -V
```
The version should be fairly new. If it's below OpenSSH 7.3 try to update it.

Make sure the .ssh directory exists in your home folder.

```bash
cd ~
mkdir -p .ssh
```

Copy the contents in [config](./config) to the `~/.ssh/config` file on your local machine.

### 2) Create key pairs for EBI

To create the key pairs on your local machine, use:

```bash
cd ~/.ssh
ssh-keygen -t rsa -f ebi_rsa -N ''
```
This command will generate two files:
- `ebi_rsa` is your private key. **Do not share it with anyone, or transmit it by
insecure means such as email!**.   
- `ebi_rsa.pub` is for other people to verify that you are in possession of your 
private key and can be shared or copied elsewhere (which is what we will do later).


### 3) Enroll in LinOTP

You need to install a Google Authenticator compliant application on your phone or computer, such as
Google Authenticator, LastPass, 1Password, Authy, WinAuth, 
Aegis (Available in F-Droid (Jan. 2020)).
You should be able to download these Apps from the Apple or Google Play Stores.

Go to https://otp.ebi.ac.uk/ and sign in with your EBI credentials. Tick
"Google Authenticator compliant" and then "entroll totp token". You can use the QR code
to add the token to your authenticator application.


### 4) Copy your public RSA keys to EBI

Now you need to copy your generated ***public*** key (the `ebi_rsa.pub` file)
from your local machine to the EBI computing clusters and two servers 
available outside the EBI network called `ligate` and `mitigate`.

You can do this from the EBI wired or wireless networks only.

### To the Codon cluster (`codon-login.ebi.ac.uk`)

The easiest way is to use `ssh-copy-id`:

```bash
ssh-copy-id -i ~/.ssh/ebi_rsa.pub <YOUR_USER_NAME>@codon-login.ebi.ac.uk
# and then add it to authorized_keys as it tells you to
```

If you do not have an `ssh-copy-id` command, you can do the following:

```bash
cat ~/.ssh/ebi_rsa.pub | ssh <YOUR_USER_NAME>@codon-login.ebi.ac.uk \
    "mkdir -p ~/.ssh; cat >> ~/.ssh/authorized_keys"
```

### To ligate and mitigate

`ligate` and `mitigate` are the two EBI SSH gateways. You can copy your key to
one or both of these servers. To ensure access to the EBI network in case one is
unavailable, copy your key to both.

First copy the base64 string in your public key (`ebi_rsa.pub`). Simply run the command below
and copy the output (except the last part that contains `blabla@blabla`).

```
$ cat ~/.ssh/ebi_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA46+cA10kQavhUu4dZzHixrzXCplf3efiZ/Zr2S4qvp8
WItF0MOjWtOWpRSR48U0jV/eOUR9R5RRn9IRRcRPR1tF1BOt0ycoM8My45WjF0JDSQ/Ij65Mw4nFZ9k
pvZ8pKa++egPm0/6Gn4FRm3DD2y8rKPdyMbyOmxryjPdQwzfwWR2XpkOEDOnbBebqAl5Drg5XaN9VNu
Zr2MH2/r8KVJe8tGntIpEAlLiI3hofXmdD1iiu+FDqtCA4k9bByUD5Taga4wiYR+cofT4dYMN08pTVj
y2VIno3FQai4OMASKdZIuiLhBeEaU0rGL8W2x3Uz5vsJoi8ylfzLRS2EoCNKyQ== blabla@blabla
```

You should only copy:

```
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA46+cA10kQavhUu4dZzHixrzXCplf3efiZ/Zr2S4qvp8
WItF0MOjWtOWpRSR48U0jV/eOUR9R5RRn9IRRcRPR1tF1BOt0ycoM8My45WjF0JDSQ/Ij65Mw4nFZ9k
pvZ8pKa++egPm0/6Gn4FRm3DD2y8rKPdyMbyOmxryjPdQwzfwWR2XpkOEDOnbBebqAl5Drg5XaN9VNu
Zr2MH2/r8KVJe8tGntIpEAlLiI3hofXmdD1iiu+FDqtCA4k9bByUD5Taga4wiYR+cofT4dYMN08pTVj
y2VIno3FQai4OMASKdZIuiLhBeEaU0rGL8W2x3Uz5vsJoi8ylfzLRS2EoCNKyQ==
```


Now login into the gate and add the key:

```bash
$ ssh -p 2244 <YOUR_USER_NAME>@ligate.ebi.ac.uk

LiTokencode: <ENTER YOUR OTP FROM YOUR AUTHENTICATOR>

gate> a

...

1. To type in the key (copy/paste)

[default=1] : 1

# paste the *base64 string* part of `cat ebi_rsa.pub` key here
# make sure there are no newlines in it
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA46+cA10kQavhUu4dZzHixrzXCplf3efiZ/Zr2S4qvp8
WItF0MOjWtOWpRSR48U0jV/eOUR9R5RRn9IRRcRPR1tF1BOt0ycoM8My45WjF0JDSQ/Ij65Mw4nFZ9k
pvZ8pKa++egPm0/6Gn4FRm3DD2y8rKPdyMbyOmxryjPdQwzfwWR2XpkOEDOnbBebqAl5Drg5XaN9VNu
Zr2MH2/r8KVJe8tGntIpEAlLiI3hofXmdD1iiu+FDqtCA4k9bByUD5Taga4wiYR+cofT4dYMN08pTVj
y2VIno3FQai4OMASKdZIuiLhBeEaU0rGL8W2x3Uz5vsJoi8ylfzLRS2EoCNKyQ==
# DON'T add the the email address at the end of the key, otherwise it will not work
# press enter and Ctrl+D here, confirm adding key by typing "yes"
```

Repeat the process above changing `ligate` for `mitigate` to also setup the other one.

Now you should be able to connect EBI by simply typing `ssh codon`.