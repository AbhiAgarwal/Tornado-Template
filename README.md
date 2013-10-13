Technology Stack
=====

- Tornado
- Nginx
- Auto-Deploy

Starting Tornado without Nginx
=====

- python main.py --port=8000, etc

Auto-Deploy (Runs on port 8005)
=====

Github -> Service Hook -> Website

- Start the server by typing “python GitAutoDeploy.py --daemon-mode”
- GitHub Service Hook URL -> "http://www.domain.com:8005"

Checking Ports
=====

Checking Ports
- netstat -nlp

Restarting Nginx
- /etc/init.d/nginx reload or service nginx restart
- /etc/init.d/nginx start
