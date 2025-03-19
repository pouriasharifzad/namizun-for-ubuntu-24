NAMIZUN (Fork for Ubuntu 24)
This project is a fork of malkemit/namizun, modified to be compatible with Ubuntu 24. The only change in this fork is ensuring that the installation works smoothly on Ubuntu 24 by fixing the setuptools module discovery issue.

This project is used to remove the limitation of asymmetric ratio for uploading and downloading Iranian servers.

Important Notice
If you have a previous or incomplete installation of namizun, you must clean up the old files before installing this fork. Run the following commands to remove previous installations:
```bash
sudo rm -rf /var/www/namizun

sudo rm /etc/systemd/system/namizun.service

sudo rm /usr/local/bin/namizun

sudo systemctl daemon-reload
```
One Line Installation Command
```bash
sudo curl https://raw.githubusercontent.com/pouriasharifzad/namizun-for-ubuntu-24/master/else/setup.sh | sudo bash
```
Manual Installation
Important Note: This fork is tested on Ubuntu 24 (Python 3.12). For older Ubuntu versions (+20), use the original repository.

You need to install pip, redis & git:
```bash
sudo apt install python3-pip python3-venv redis git -y
```
Note: Sometimes Redis does not start automatically, start it with the following command:
```bash
sudo systemctl start redis.service
```
You need to create a directory to clone the project:
```bash
mkdir -p /var/www/namizun && cd /var/www/namizun
```
Clone the project with Git:
```bash
git init

git remote add origin https://github.com/pouriasharifzad/namizun-for-Ubuntu-24.git

git pull origin master
```
Make a virtual environment:
```bash
python3 -m venv /var/www/namizun/venv
```
Install the project requirements with pip by setup.py (namizun_core & namizun_menu):
```bash
cd /var/www/namizun && source /var/www/namizun/venv/bin/activate && pip install wheel && pip install namizun_core/ namizun_menu/ && deactivate
```
Create a service for uploader.py (for running namizun script):
```bash
ln -s /var/www/namizun/else/namizun.service /etc/systemd/system/
```
Reload the service files to include the new service and start namizun.service:
```bash
sudo systemctl daemon-reload && sudo systemctl enable namizun.service && sudo systemctl start namizun.service
```
Create namizun command to execute menu.py:
```bash
ln -s /var/www/namizun/else/namizun /usr/local/bin/ && chmod +x /usr/local/bin/namizun
```
