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
