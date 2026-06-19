# ============================================================
# Dockerfile for AI Chatbot UI (Nova AI)
# Serves static HTML + CSS with Nginx
# ============================================================

# ---- Stage 1: Build stage (if needed, but we keep it simple) ----
# Use official Nginx image as base
FROM nginx:alpine

# ---- Metadata ----
LABEL maintainer="Your Name <your.email@example.com>"
LABEL description="Nova AI Chatbot UI - Static web interface"
LABEL version="1.0.0"

# ---- Environment variables ----
ENV NGINX_PORT=80 \
    NGINX_ROOT=/usr/share/nginx/html

# ---- Remove default Nginx static files ----
RUN rm -rf /usr/share/nginx/html/*

# ---- Copy our static files ----
# Copy index.html, style.css, and any other assets
COPY index.html /usr/share/nginx/html/
COPY style.css /usr/share/nginx/html/

# ---- Optional: Copy custom Nginx config if needed ----
# If you have a custom nginx.conf, uncomment the following:
# COPY nginx.conf /etc/nginx/conf.d/default.conf

# ---- Expose port 80 ----
EXPOSE 80

# ---- Health check ----
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD wget --quiet --tries=1 --spider http://localhost/ || exit 1

# ---- Start Nginx (default CMD from base image) ----
# The base image already has CMD ["nginx", "-g", "daemon off;"]
# so we don't need to override it.

# ---- Instructions to build and run ----
# Build: docker build -t nova-chatbot-ui .
# Run:   docker run -d -p 8080:80 --name nova-chatbot nova-chatbot-ui
# Access: http://localhost:8080

# ============================================================
# ALTERNATIVE: Multi-stage build for more complex setups
# ============================================================
#
# If you want to use a custom Nginx config, create a file named
# `nginx.conf` in the same directory with this content:
#
# server {
#     listen 80;
#     server_name localhost;
#     root /usr/share/nginx/html;
#     index index.html;
#
#     location / {
#         try_files $uri $uri/ /index.html;
#     }
#
#     # Gzip compression
#     gzip on;
#     gzip_types text/css text/javascript application/javascript;
# }
#
# Then uncomment the COPY line above.

# ============================================================
# DOCKER COMPOSE EXAMPLE (optional)
# ============================================================
#
# Create a docker-compose.yml file:
#
# version: '3.8'
# services:
#   chatbot-ui:
#     build: .
#     container_name: nova-chatbot
#     ports:
#       - "8080:80"
#     restart: unless-stopped
#     healthcheck:
#       test: ["CMD", "wget", "--quiet", "--tries=1", "--spider", "http://localhost/"]
#       interval: 30s
#       timeout: 3s
#       retries: 3
#
# Run: docker-compose up -d

# ============================================================
# NOTES:
# - This Dockerfile assumes index.html and style.css are in the
#   same directory as the Dockerfile.
# - The Nginx Alpine image is lightweight (~20MB).
# - For production, consider adding security headers and SSL.
# - You can also serve the files with a simple HTTP server like
#   'python -m http.server' or 'serve' if you prefer.
# ============================================================
