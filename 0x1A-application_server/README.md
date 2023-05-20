Application Server
This project involved deploying our AirBnB clone application. I set up Nginx on the web servers provided by Holberton School to serve a WSGI Flask app running through Gunicorn. Additionally, I configured an Upstart script to ensure the application runs automatically after server reboots.

Tasks:
Task 0: Set up development with Python

For this task, I configured the file web_flask/0-hello_route.py from my AirBnB_clone_v2 project to serve content on the route /airbnb-onepage/ running on port 5000.
Task 1: Set up production with Gunicorn

This task involved setting up a production environment and installing/configuring Gunicorn to serve the same file from Task 0.
Task 2: Serve a page with Nginx

File: 2-app_server-nginx_config
This task required configuring the Nginx server to proxy requests on the route /airbnb-onepage/ to the Gunicorn app running on port 5000.
Task 3: Add a route with query parameters

File: 3-app_server-nginx_config
Here, the Nginx configuration file was updated to proxy requests on the route /airbnb-dynamic/number_odd_or_even/<int:num> to the Gunicorn app running on port 5000.
Task 4: Let's do this for your API

For this task, I configured the API from my AirBnB_clone_v3 project to run on Gunicorn.
File: 4-app_server-nginx_config
The Nginx configuration file was updated to proxy requests on the AirBnB API to the corresponding Gunicorn app.
Task 5: Serve your AirBnB clone

This task involved configuring the complete AirBnB app from AirBnB_clone_v4 to run on Gunicorn and be served through Nginx.
File: 5-app_server-nginx_config
The Nginx configuration file was updated to serve the static assets from web_dynamic/static/ on the Gunicorn AirBnB app.
Task 6: Deploy it

File: gunicorn.conf
I created a configuration file for an Upstart script that starts a Gunicorn process bound to port 5003, serving the content from Task 5.
The Gunicorn process spawns three worker processes and logs errors to /tmp/airbnb-error.log while access logs are saved to /tmp/airbnb-access.log.
Task 7: No service interruption

File: 4-reload_gunicorn_no_downtime
A Bash script was provided to gracefully reload Gunicorn without causing any service interruption.




