# MSSQL-instllation-on-ubuntu-22.04-server
MSSQL instllation on ubuntu 22.04 server

Download the public key, convert from ASCII to GPG format, and write it to the required location:
```
curl -fsSL https://packages.microsoft.com/keys/microsoft.asc | sudo gpg --dearmor -o /usr/share/keyrings/microsoft-prod.gpg
```
If you receive a warning about the public key not being available, you can use the following command instead:
```
curl https://packages.microsoft.com/keys/microsoft.asc | sudo tee /etc/apt/trusted.gpg.d/microsoft.asc
```
Manually download and register the SQL Server Ubuntu repository:
```
curl -fsSL https://packages.microsoft.com/config/ubuntu/22.04/mssql-server-preview.list | sudo tee /etc/apt/sources.list.d/mssql-server-preview.list
```
Run the following commands to install SQL Server:
```
sudo apt-get update
sudo apt-get install -y mssql-server
````
After the package installation finishes, run mssql-conf setup and follow the prompts to set the sa password and choose your edition. As a reminder, the following SQL Server editions are freely licensed: Evaluation, Developer, and Express.
```
sudo /opt/mssql/bin/mssql-conf setup
```
Once the configuration is done, verify that the service is running:
```
systemctl status mssql-server --no-pager
systemctl enable mssql-server

passwd mssql
```
    If you plan to connect remotely, you might also need to open the SQL Server TCP port (default 1433) on your firewall.

At this point, SQL Server is running on your Ubuntu machine and is ready to use.

Install the SQL Server command-line tools

Enter superuser mode.
```
sudo su
```
Import the public repository GPG keys.
```
curl https://packages.microsoft.com/keys/microsoft.asc | sudo tee /etc/apt/trusted.gpg.d/microsoft.asc
```
Register the Microsoft Ubuntu repository.
```
curl https://packages.microsoft.com/config/ubuntu/22.04/prod.list | tee /etc/apt/sources.list.d/mssql-release.list
```
Exit superuser mode.
```
exit
```
Update the sources list and run the installation command with the unixODBC developer package.
```
sudo apt-get update
sudo apt-get install mssql-tools18 unixodbc-dev
```
To update to the latest version of mssql-tools, run the following commands:
```
sudo apt-get update
sudo apt-get install mssql-tools18
```
Optional: Add /opt/mssql-tools18/bin/ to your PATH environment variable in a bash shell.

To make sqlcmd and bcp accessible from the bash shell for login sessions, modify your PATH in the ~/.bash_profile file with the following command:
```
echo 'export PATH="$PATH:/opt/mssql-tools18/bin"' >> ~/.bash_profile
source ~/.bash_profile
```
To make sqlcmd and bcp accessible from the bash shell for interactive/non-login sessions, modify the PATH in the ~/.bashrc file with the following command:
```
echo 'export PATH="$PATH:/opt/mssql-tools18/bin"' >> ~/.bashrc
source ~/.bashrc
```
Run sqlcmd with parameters for your SQL Server name (-S), the user name (-U), and the password (-P). In this tutorial, you connect locally, so the server name is localhost. The user name is sa and the password is the one you provided for the sa account during setup.
```
sqlcmd -S localhost -U sa -P '<password>' -C
```
Additonal mssqltool
# Microsoft GPG key
```
curl https://packages.microsoft.com/keys/microsoft.asc | sudo tee /etc/apt/trusted.gpg.d/microsoft.asc
```
# Ubuntu 22.04 for repo  (version 17)
```
curl https://packages.microsoft.com/config/ubuntu/22.04/prod.list | sudo tee /etc/apt/sources.list.d/mssql-release.list
```
## package update
```
sudo apt-get update
```

# version 17 install
```
sudo ACCEPT_EULA=Y apt-get install mssql-tools unixodbc-dev

echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
source ~/.bash_profile

echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
```

version 17 path = /opt/mssql-tools/bin

version 18 path = /opt/mssql-tools18/bin




