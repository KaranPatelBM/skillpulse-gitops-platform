FROM nginx:1.28-alpine

# Copy static files
COPY index.html /usr/share/nginx/html/
COPY css /usr/share/nginx/html/css
COPY js /usr/share/nginx/html/js

# Copy nginx configs
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY nginx-main.conf /etc/nginx/nginx.conf

# Create non-root user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Create writable dirs
RUN mkdir -p /tmp/nginx /var/cache/nginx /var/log/nginx

# Grant permissions
RUN chown -R appuser:appgroup \
    /usr/share/nginx/html \
    /tmp/nginx \
    /var/cache/nginx \
    /var/log/nginx \
    /etc/nginx

# Switch user
USER appuser

EXPOSE 8084

HEALTHCHECK --interval=30s --timeout=5s --retries=3 \
  CMD wget --spider -q http://localhost:8084 || exit 1

CMD ["nginx", "-g", "daemon off;"]