In this project i placed a server behind a load balancer, and creating a custom NGINX response header, this way it will be possible to track which web server is answering our HTTP requests, to understand and track the way a load balancer works.

# Task 1
- Configure NGinx so that its HTTP response contains a custom header
    name of Custom HTTP should be "X-Served-By", value=hostname of sever Nginx is runnnig on.
- 0-custom_response_header so that it configures a brand new ubuntu machine (Ignore SC2154 for shellcheck)

# Task 2
- 