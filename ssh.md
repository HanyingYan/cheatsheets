## 1. SSH
**Secure Shell**, or SSH, is a network protocol that gives users a secure way to access a computer over an unsecured network.<br/>
Let's use Google Cloud Platform Virtual Machine for example to show how to use ```ssh```.

### A. Generate keys
Use the ]```ssh-keygen```](https://cloud.google.com/compute/docs/connect/create-ssh-keys) command to generate a public/private authentication key pair.<br/>
Authentication keys allow a user to connect to a remote system without supplying a password.
```
ssh-keygen -t rsa -f ~/.ssh/gcp -C hanying -b 2048
```
* ```-t``` specify the key type
* ```-f``` specify the output keyfile name
* ```-c``` specify the username
* ```-b``` specify the bits number

### B. Upload Key
Upload the public key to GCP VM, in our case, it is the ```./ssh/gcp.pub``` <br/>
Note: we should protect our private key and don't put in any shared public place.<br/>
Now if we run ```ssh -i ~/.ssh/gcp hanying@<vm_external_ip_address>``` we can log in to our VM.

### C. Setup config
We can allso setup ```config``` file to easy login next time: ```touch config``` and then add the part below.
```		
Host <host_name>
    HostName <vm_external_ip_address>
    User hanying
    IdentityFile /Users/hanying/.ssh/gcp
```
Now we can use ```ssh <host_name>``` to log in to our VM.


## 2. SFTP
**Secure File Transfer Protocol**, or SFTP, is a secure file transfer protocol that uses SSH encryption to provide a high level of security for sending and receiving file transfers.

If ```ssh <host_name>``` works, we can then establish an SFTP session by  ```sftp <host_name>```<br/>
We should have a command prompt similar to ```sftp>```, and use the following code to transfer files
1. upload the file from local dir to remote dir
```
sftp> cd <remote_dir_1>
sftp> put <local_dir_1>/<file_name>
```
2. download the file on remote server to local system
```
sftp> get <remote_dir_2>/<file_name_2>
```
3. upload and download directories by using the -r parameter.
```
sftp> put -r  local_folder 
sftp> get -r  remote_folder
```


## 3. SCP
**Secure Copy**, or SCP, is also a means of securely transferring files between a local host and a remote host, or between two remote hosts based on SSH.

If ```ssh <host_name>``` works, then
1. Upload the file from local dir to remote dir
```
scp <local_dir>/<file_name> <host_name>:<remote_dir>
```
2. download the file on remote server to local system
```
scp <host_name>:<remote_dir> <local_dir>/<file_name> 
```
3. using the -r parameter for folders
```
scp -r <local_folder> <host_name>:<remote_dir>
scp -r <host_name>:<remote_dir> <local_folder> 
```
