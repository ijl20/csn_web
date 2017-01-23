# Cambridge Sensor Network Portal

This project provides a multi-user portal for the management of sensors on
the Cambridge Sensor Network.

The portal is designed to accomodate self-provisioning of sensors that will
be registered on the CSN Lorawan (Low-power, Long-Range) network of radio
gateways in the Cambridge UK region.

The portal has three main areas of function:
* User management - these are the people able to register devices and manage the
receipt of the data.
* Device management - this is where devices are registered and the server designated to
receive their data.
* Server management - this is where user servers are defined that can then be used to receive data from
the sensors.

## User Management

## Device Management

## Server Management

## Installation
```
python3 -m venv csn_web_venv
mkdir csn_web
cd csn_web
source ~/csn_web_venv/bin/activate
python3 -m pip install django
python3 -m pip install --upgrade pip
django-admin.py startproject csn_web
git init

cp ../tfc_web/.gitignore .
git add --all .
git commit -m "Initial csn_web project start"
python3 -m pip install gunicorn
cd csn_web
gunicorn --bind localhost:8099 csn_web.wsgi
python3 -m pip install whitenoise

# install postgresql
sudo apt update
sudo apt upgrade
sudo apt install postgresql postgresql-contrib libpq-dev python-dev

sudo -u postgres psql

sudo -u postgres createdb csn_prod
sudo -u postgres createuser csn_prod --interactive
sudo adduser csn_prod
sudo -u csn_prod psql

# setup nginx for https://<host>/csn

sudo cp csn_web/config/nginx/includes/csn_web_port_443.conf /etc/nginx/includes/
sudo service nginx restart

python3 -m pip install psycopg2

ssh csn_prod@localhost
ssh-keygen -t rsa -C "csn_prod@tfc-app2"
sudo cp ~/.ssh/authorized_keys /home/csn_prod/.ssh
sudo chown csn_prod:csn_prod /home/csn_prod/.ssh/authorized_keys
