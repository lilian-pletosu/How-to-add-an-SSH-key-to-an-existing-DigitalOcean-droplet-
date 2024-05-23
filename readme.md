# How to add an SSH key to an existing DigitalOcean droplet


This is a quick and easy method to add the SSH key of your current machine to an existing droplet.
## 1. Retrieve and save your current public key to a text file

* ####  Generate keypair (OPTIONAL)
In case your RSA keypair is not generated yet or you want to generate new keys, simply enter this and follow the instructions:

```
ssh-keygen -t rsa
```

* ####  Save SSH key to a separate file
Enter the following commands in your terminal:

```
cd ~
cat ~/.ssh/id_rsa.pub > key.txt
```

## 2. Upload the SSH key to a file sharing service

```
curl https://bashupload.com/key.txt --data-binary @key.txt
```

This will give you a link that you can use to download the key. Copy the link and keep it somewhere safe.
## 3. Reset your droplet's password

* ####  Reset droplet password

If you don't have your droplet's password (which will be the case if you kept SSH as the default access mechanism) then you can reset it.

Sign in to DigitalOcean > Open the droplet > Click Access > Reset root password

Your password will be mailed to you. Keep the email open so you can look at the password and type it in on the next step.

* #### Set a new password
Click on "**Console**" on the top right to open the droplet's console. Enter **root** in the terminal, and then carefully type in the password specified in the email. The DigitalOcean console does not allow you to copy-paste so this operation is a little annoying.

  Follow the instructions in the terminal to set a new UNIX password (**_and keep this password somewhere safe_**).

## 4. Add SSH key to droplet

  * ####  Run commands as specific user (OPTIONAL)
If you want to add the SSH key for a specific user, you will have to type in the following to execute commands as that user.

```
su - <username>
```
  
* #### Append SSH key to droplet

You will need the link obtained in Step 2 now.

```
cd ~/.ssh
wget <link-from-step-2>
cat key.txt >> authorized_keys
```

Make sure you use **>>** so the new key is appended to the authorized_keys file.

You can now open your terminal and type in

```
ssh <user>@<ip>
```
or
```
ssh -i ./<your_key_name> <user>@<droplet_api>

```

and you should be able to access your DigitalOcean droplet normally.
