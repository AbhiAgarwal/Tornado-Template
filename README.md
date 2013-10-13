Technology Stack
=====

- Tornado
- Nginx
- Auto-Deploy

Starting Tornado
=====

- python main.py --port=8000
- python main.py --port=8001
- python main.py --port=8002
- python main.py --port=8003

Auto-Deploy (Runs on port 8005)
=====

Github -> Service Hook -> Website

- Start the server by typing “python GitAutoDeploy.py --daemon-mode”
- GitHub Service Hook URL -> "http://www.websitename.com:8005"

Checking Ports
=====

Checking Ports
- netstat -nlp

Restarting Nginx
- /etc/init.d/nginx reload
- /etc/init.d/nginx start
- service nginx restart
