---
layout: post
title: Nginx Request Rate Limit
author: digvijayb
tags:
  - nginx
  - web
  - ratelimit
date: 2023-03-25T09:59:42.780Z
description: Nginx configuration file that implements rate limiting with a limit of 50 requests per minute per IP address and returns a 429 error code when the limit is exceeded
thumbnail: /images/uploads/featured.png
---
Nginx configuration file that implements rate limiting with a limit of 50 requests per minute per IP address and returns a 429 error code when the limit is exceeded:

<!-- more -->

```conf
http {
  # Define a limit zone named "my_zone" that tracks requests by the client IP address
  limit_req_zone $binary_remote_addr zone=my_zone:10m rate=50r/m;

  # Server block that handles requests
  server {
    listen 80;
    server_name example.com;

    # Limit requests to 50 per minute per IP address
    limit_req zone=my_zone burst=10 nodelay;

    # Return a 429 error code when the limit is exceeded
    limit_req_status 429;

    # Your other server configuration goes here...
  }
}
```
## Expained

In this configuration, the `limit_req_zone` directive defines a shared memory zone named "my_zone" that will track requests by the client IP address. The `$binary_remote_addr` variable is used to obtain the client IP address in binary form, which is more efficient than using the `$remote_addr` variable.

The `limit_req` directive is used to limit requests to 50 per minute per IP address. The `burst` parameter specifies the maximum number of requests that are allowed to exceed the rate limit before requests are delayed, and the `nodelay` parameter ensures that requests are not delayed when the limit is first exceeded.

The `limit_req_status` directive specifies the HTTP status code that should be returned when the limit is exceeded. In this case, it is set to 429, which indicates "Too Many Requests".

You can adjust the values of the `limit_req_zone` and `limit_req` directives to suit your specific needs. For example, you may want to increase or decrease the rate limit, adjust the burst size, or use a different tracking variable (such as a cookie) instead of the client IP address.