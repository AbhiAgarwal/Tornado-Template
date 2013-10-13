Tornado Template
================================

Easy to use Tornado template. This stack uses:

- Tornado
- Nginx
- Auto-Deploy
- Twitter Bootstrap

### Installing Git, Python Tools, Nginx, Tornado, and Supervisor

This is using Ubuntu 10.04+

Installing the Tools:

`apt-get install python-setuptools`,
`easy_install pip`,
`pip install tornado`,
`apt-get install git`,
`apt-get install nginx`,
`pip install supervisor`

Create Directory:

`mkdir /srv/www`
`mkdir /srv/www/domainname.com `,
`cd /srv/www/domainname.com`,
`git clone git@github.com:AbhiAgarwal/Tornado-Template.git`

Change `nginx/nginx.conf` and `supervisord/supervisord.conf` to point to your `/srv/www/domainname.com/` to your directory path. Do this before configuring them or they will mess up.

Creating configuration files:

`cd /etc/nginx`,
`rm nginx.conf`,
`ln -s /srv/www/domainname.com/nginx/nginx.conf nginx.conf`,
`cd`,
`ln -s /srv/www/domainname.com/supervisord/supervisord.conf supervisord.conf`

Setting up Nginx:

`adduser --system --no-create-home --disabled-login --disabled-password --group nginx`,
`mkdir ~/logs`,
`supervisord`,
`/etc/init.d/nginx start`

It's started the Nginx server now, and started the webserver at port 8000, 8001, 8002, 8003. 

Now look at Auto-Deploy and set that up. If you don't want to use that then:

`cd /srv/www/domainname.com/`,
`git pull`

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

### Checking Ports ###

Checking Ports
- `netstat -nlp`

Restarting Nginx
- `/etc/init.d/nginx reload` or `service nginx restart`
- `/etc/init.d/nginx start`

## Problems

- Problems with Supervisord?
    - try: `cd`, `unlink supervisord.sock`
