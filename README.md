Tornado Template
================================

Easy to use Tornado template. This stack uses:

- Tornado
- Nginx
- Auto-Deploy
- Twitter Bootstrap

Installing this should take roughly **5 minutes**!

### Installing Git, Python Tools, Nginx, Tornado, and Supervisor

This is using Ubuntu 10.04+

**Installing the Tools**:

```
apt-get install python-setuptools
easy_install pip
pip install tornado
apt-get install git
apt-get install nginx
pip install supervisor
```

If git doesn't work then: `sudo apt-get -y install git-core`

**Setting up your Github Account**:

```
cd ~/.ssh
ls
ssh-keygen -t rsa -C "email@email.com"
vim id_rsa.pub
```

Copy the public key, paste it into your GitHub account SSH Key section, then try:
```
ssh -T git@github.com
```

**Create Directory**:

```
mkdir /srv/www
mkdir /srv/www/domainname.com 
cd /srv/www/domainname.com
git clone git@github.com:AbhiAgarwal/Tornado-Template.git /srv/www/domainname.com/
```

Remember to add `/srv/www/domainname.com/` to the `clone` so it doesn't create a new directory.

Change `nginx/nginx.conf` and `supervisord/supervisord.conf` to point to your `/srv/www/domainname.com/` to your directory path. Do this before configuring them or they will mess up.

**Creating configuration files**:

```
cd /etc/nginx
rm nginx.conf
ln -s /srv/www/domainname.com/nginx/nginx.conf nginx.conf
cd
ln -s /srv/www/domainname.com/supervisord/supervisord.conf supervisord.conf
```

**Setting up Nginx:**

```
adduser --system --no-create-home --disabled-login --disabled-password --group nginx
mkdir ~/logs
supervisord
/etc/init.d/nginx start
```

It's started the Nginx server now, and started the webserver at port 8000, 8001, 8002, 8003. 

Try and open your URL/IP and it should work!

**Now look at Auto-Deploy and set that up. If you don't want to use that then:**

```
cd /srv/www/domainname.com/
git pull
```

### Starting Tornado

Using this Tornado template without Implementing Nginx:

`python main.py --port=80`

Using this Tornado template using Nginx:

`/etc/init.d/nginx start`

### Auto-Deploy (Runs on port 8005) - [Link](https://github.com/logsol/Github-Auto-Deploy) ###

Github -> Service Hook -> Website

- Update the file (GitAutoDeploy.conf.json)
    - Change `url` and `path`

- Start the server by typing:
    - `python GitAutoDeploy.py --daemon-mode`
- GitHub Service Hook URL
    - `http://www.domain.com:8005`

### Generating the Secret Key ###

If you want to generate a secret key for the cookie_secret on your main file then:
```
import base64
import uuid
print base64.b64encode(uuid.uuid4().bytes + uuid.uuid4().bytes)
```

### Checking Ports ###

**Checking Ports**
- `netstat -nlp`

**Restarting Nginx**
- `/etc/init.d/nginx reload` or `service nginx restart`
- `/etc/init.d/nginx start`

## Problems

- Problems with Supervisord?
    - try: `cd`, `unlink supervisord.sock`

## Todo

[] Create a .sh script to install all of it together