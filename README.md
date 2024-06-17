# Deploying Flask App Behind HAProxy

## Overview:
This Ansible playbook is designed to deploy a Flask application behind an HAProxy load balancer on a group of web servers. The Flask application serves a simple response, and HAProxy is used to distribute incoming traffic across multiple backend servers.

## Prerequisites:
- Ansible installed on your local machine.
- SSH access to the target hosts configured with SSH keys.
- Flask application files present in the current working directory.
- HAProxy configuration template file (haproxy.cfg.j2) present in the current working directory.
- ngnix configuration templete file (ngnix_udp_load_balancer.conf.j2) in the current directory
- snmpd configuration remplate file (snmpd.conf.j2) in the current directory

## Setup:
1. Ensure that the Flask application files (application2.py) are located in the current working directory.
2. Make sure the HAProxy configuration template file (haproxy.cfg.j2) is also present in the current working directory.

## Usage:
1. Update the `hosts` file with the IP addresses or hostnames of your web servers and HAProxy server.
2. Run the Ansible playbook using the following command:
    ```
    ansible-playbook -i hosts site.yaml
## Description:
### Tasks
Updates package lists on all managed hosts.
- Installs HAproxy on a dedicated server for load balancing.
- Gathers IP addresses of web servers for HAproxy configuration.
- Configures HAproxy using a Jinja2 template for dynamic configuration management.
- Installs Python dependencies (pip, Flask, Gunicorn) on web servers for application execution.
- Creates a directory for the Flask application on web servers.
- Deploys the Flask application code (application2.py) to web servers.
- Runs the Flask application as a daemon using Gunicorn for efficient resource utilization. 
- Installs and configures SNMPd daemon on the webservers group in hosts file
- Installs and configures Nginx for UDP load balancing,

## Notes:
- Customize the HAProxy configuration template (`haproxy.cfg.j2`) according to your requirements.
- Ensure that SSH keys are properly configured for passwordless authentication to the target hosts.
- For configuring SNMPd and Nginx, you will need to create and use template files (snmpd.conf.j2 for SNMPd and udp_load_balancer.conf.j2 for Nginx) with the appropriate configurations.
- Test the deployment thoroughly to ensure the Flask application is accessible through the HAProxy load balancer.

## References:**
- Flask Documentation: [https://flask.palletsprojects.com/](https://flask.palletsprojects.com/)
- HAProxy Documentation: [https://www.haproxy.com/documentation/](https://www.haproxy.com/documentation/)