---
title: Net debug
hide:
  # - navigation
  # - toc
---

## Overview

Example to enable Net debug  , compile with the following flags 

-D WLED_DEBUG 

-D WLED_DEBUG_HOST='"192.168.x.y"' ;; to send debug messages over network to host 192.168.x.y - FQDN is also possible

-D WLED_DEBUG_NET_PORT=1878 ;; port for network debugging. default = 7868


To access net debug from the host type the following  netcat   example : 

nc -l 1878 -u

Debug can be switched on and off in the Info tab:

<img width="440" alt="image" src="https://user-images.githubusercontent.com/91013628/220674439-e3f73a68-4557-499b-b240-e46bdac1d561.png">
