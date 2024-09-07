# AirBnB Clone v2 - Application Server Setup

## Project Overview

This project involves setting up a web application server for the AirBnB clone v2 using Nginx and Gunicorn. You will configure both development and production environments, proxy requests, and handle multiple routes and services.

## Background Context

You will extend your existing web infrastructure by integrating an application server (Gunicorn) with Nginx to serve your AirBnB clone project. Nginx will act as a reverse proxy, forwarding requests to Gunicorn, which will handle dynamic content.

## Resources

- [Application server vs web server](#)
- [How to Serve a Flask Application with Gunicorn and Nginx on Ubuntu 16.04](#) (Avoid using virtualenv for Gunicorn; install everything globally)
- [Running Gunicorn](#)
- [Flask strict_slashes management](#)
- [Upstart documentation](#)

## Requirements

### General

- A `README.md` file at the root of your project folder is mandatory.
- Everything Python-related must be done using `python3`.
- All config files must have comments.

### Bash Scripts

- All your files will be interpreted on Ubuntu 16.04 LTS.
- All files should end with a new line.
- All Bash script files must be executable.
- Your Bash script must pass Shellcheck (version 0.3.7-5~ubuntu16.04.1 via `apt-get`) without any error.
- The first line of all Bash scripts should be exactly `#!/usr/bin/env bash`.
- The second line of all Bash scripts should be a comment explaining what the script does.

## Tasks

### 0. Set up Development with Python

- Ensure task #3 of your SSH project is completed for `web-01`. The checker will connect to your servers.
- Install the `net-tools` package on your server: `sudo apt install -y net-tools`.
- Git clone your AirBnB_clone_v2 on your `web-01` server.
- Configure the file `web_flask/0-hello_route.py` to serve its content from the route `/airbnb-onepage/` on port 5000.
- Your Flask application object must be named `app`.

**Example Command:**

```bash
python3 -m web_flask.0-hello_route

## 1. Set up Production with Gunicorn

- Install Gunicorn and any other libraries required by your application.
- The Flask application object should be called `app`.
- Serve the same content from the same route as in the previous task using Gunicorn on port 5000.
- Ensure nothing is listening on port 6000.

**Example Command:**

```bash
gunicorn --bind 0.0.0.0:5000 web_flask.0-hello_route:app

2. Serve a Page with Nginx

    Configure Nginx to serve your page from the route /airbnb-onepage/.
    Nginx should proxy requests to the process listening on port 5000.
    Include your Nginx config file as 2-app_server-nginx_config.

Example Commands:

    Start Gunicorn:

bash

gunicorn --bind 0.0.0.0:5000 web_flask.0-hello_route:app

    Test with curl:

bash

curl 127.0.0.1/airbnb-onepage/

3. Add a Route with Query Parameters

    Add another service for Gunicorn to handle requests to /airbnb-dynamic/number_odd_or_even/<int:n>.
    Configure Nginx to proxy requests to the route /airbnb-dynamic/number_odd_or_even/(any integer) to a Gunicorn instance on port 5001.
    Include your Nginx config file as 3-app_server-nginx_config.

Example Commands:

    Start Gunicorn instances:

bash

tmux new-session -d 'gunicorn --bind 0.0.0.0:5000 web_flask.0-hello_route:app'
tmux new-session -d 'gunicorn --bind 0.0.0.0:5001 web_flask.6-number_odd_or_even:app'

    Test with curl:

bash

curl 127.0.0.1:5001/number_odd_or_even/6

4. Serve Your API

    Git clone your AirBnB_clone_v3.
    Set up Nginx to route /api/ to a Gunicorn instance on port 5002.
    Test your setup with Gunicorn bound to api/v1/app.py.
    Include your Nginx config as 4-app_server-nginx_config.

Example Commands:

    Start Gunicorn:

bash

tmux new-session -d 'gunicorn --bind 0.0.0.0:5002 api.v1.app:app'

    Test with curl:

bash

curl 127.0.0.1:5002/api/v1/states

5. Serve Your AirBnB Clone

    Git clone your AirBnB_clone_v4.
    Your Gunicorn instance should serve content from web_dynamic/2-hbnb.py on port 5003.
    Set up Nginx to route requests to the root / and serve static assets from web_dynamic/static/.
    Ensure the correct IP is configured in web_dynamic/static/scripts/2-hbnb.js.
    Include your Nginx config as 5-app_server-nginx_config.

Example Commands:

    Start Gunicorn:

bash

gunicorn --bind 0.0.0.0:5003 web_dynamic.2-hbnb:app

    Test with curl:

bash

curl 127.0.0.1:5003

License

Copyright © 2024 ALX, All rights reserved