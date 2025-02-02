# Nginx
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


# Nginx Configuration Guide

This guide provides a comprehensive overview of Nginx configuration with examples, troubleshooting commands, and instructions for contributing.

## 🔧 Understanding the Configuration File

Nginx configurations consist of directives categorized into:

### 📌 Simple Directives
- End with a semicolon.
- Example:
  ```nginx
  worker_connections 1024;
  ```

### 📌 Block Directives
- Use `{}` and may contain nested directives.
- Example:
  ```nginx
  http {
      server {
          listen 80;
          server_name example.com;

          location / {
              root /var/www/html;
              index index.html;
          }
      }
  }
  ```

## 🖼️ Serving Static Content

### Basic Configuration Example:
```nginx
server {
    listen 80;
    server_name example.com;

    location / {
        root /data/www;
        index index.html;
    }

    location /images/ {
        root /data;
    }
}
```

### How It Works:
- 📌 Requests to `/` → Serve files from `/data/www/`
- 📌 Requests to `/images/` → Serve files from `/data/images/`
- 📌 If the file is missing → Returns a 404 error

## 🔄 Setting Up a Simple Proxy Server

### Basic Reverse Proxy Configuration:
```nginx
server {
    listen 80;

    location / {
        proxy_pass http://localhost:8080;
    }

    location ~ \.(gif|jpg|png)$ {
        root /data/images;
    }
}
```

### How It Works:
- 🔄 Requests for `/` → Forwarded to `http://localhost:8080`
- 🖼️ Requests for `.gif`, `.jpg`, `.png` → Served from `/data/images`

## ⚡ FastCGI Proxying

### Basic FastCGI Configuration:
```nginx
server {
    listen 80;

    location / {
        fastcgi_pass localhost:9000;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param QUERY_STRING $query_string;
        include fastcgi_params;
    }

    location ~ \.(gif|jpg|png)$ {
        root /data/images;
    }
}
```

### How It Works:
- ⚡ PHP requests → Forwarded to `localhost:9000` (PHP-FPM)
- 🖼️ Image files → Served from `/data/images`

## 🛠️ Troubleshooting

### Common Nginx Troubleshooting Commands:
- ✅ Check error logs:
  ```bash
  tail -f /var/log/nginx/error.log
  ```
- ✅ Test configuration syntax:
  ```bash
  nginx -t
  ```
- ✅ Check if Nginx is running:
  ```bash
  systemctl status nginx
  ```
- ✅ Restart Nginx:
  ```bash
  systemctl restart nginx
  ```

## 📚 Resources

- [Official Nginx Documentation](https://nginx.org/en/docs/)
- [Nginx Configuration Generator](https://nginxconfig.io/)
- [Nginx Community Forum](https://forum.nginx.org/)
- [Nginx Error Logs](https://nginx.org/en/docs/)

## 🤝 Contributing

🚀 Contributions are welcome! Feel free to fork this repository, submit issues, or create pull requests.

### How to Contribute:
1️⃣ Fork the repo  
2️⃣ Create a new branch (e.g., `git checkout -b feature-branch`)  
3️⃣ Commit changes (`git commit -m "Added new feature"`)  
4️⃣ Push to GitHub (`git push origin feature-branch`)  
5️⃣ Open a pull request

## ⚖️ License

📜 This project is licensed under the MIT License – see the LICENSE file for details.

🔥 Enjoy using Nginx! If this guide helped you, give it a ⭐ on GitHub! 🚀✨

## How to Use This File
- Copy the entire content above.
- Create a new repository on GitHub.
- Add a `README.md` file.
- Paste the copied content and commit!

This `README.md` is GitHub-ready, well-structured, and formatted for readability. Let me know if you need any tweaks! 🚀

## ⚙️ Start, Stop & Reload  

```sh
nginx        # Start  
nginx -s quit  # Stop (gracefully)  
nginx -s stop  # Stop (immediately)  
nginx -s reload  # Reload configuration  
ps -ax | grep nginx  # Check running processes  
nginx -t  # Test configuration


