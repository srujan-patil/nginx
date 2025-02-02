# nginx
# 🚀 Beginner’s Guide to Nginx  

A concise guide to **starting, stopping, reloading configurations**, **serving static content**, **proxy server setup**, and **FastCGI proxying**.  

## 📖 Table of Contents  
- [Introduction](#introduction)  
- [Start, Stop & Reload](#start-stop--reload)  
- [Configuration Structure](#configuration-structure)  
- [Serving Static Content](#serving-static-content)  
- [Proxy Server](#proxy-server)  
- [FastCGI Proxying](#fastcgi-proxying)  
- [Troubleshooting](#troubleshooting)  

---

## 📌 Introduction  

**Nginx** is a **high-performance web server** used for static content serving, load balancing, and proxying.  
📍 **Configuration file location:** `/etc/nginx/nginx.conf`  

---

## ⚙️ Start, Stop & Reload  

```sh
nginx        # Start  
nginx -s quit  # Stop (gracefully)  
nginx -s stop  # Stop (immediately)  
nginx -s reload  # Reload configuration  
ps -ax | grep nginx  # Check running processes  
nginx -t  # Test configuration  
