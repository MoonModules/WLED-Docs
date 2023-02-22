---
title: Net debuf
hide:
  # - navigation
  # - toc
---

## Overview

Example to enable Net debug  , compile with the following flags 
-D WLED_DEBUG 
-D WLED_DEBUG_HOST='"192.168.x.y"' ;; to send debug messages over network to host 192.168.x.y - FQDN is also possible
-D WLED_DEBUG_NET_PORT=7878 ;; port for network debugging. default = 7868


To access net debug from the host type the following  netcat   example : 
nc -l  7878  -u