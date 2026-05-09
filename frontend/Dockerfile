FROM nginx:1.28-alpine

# Copy static files
COPY index.html /usr/share/nginx/html/
COPY css /usr/share/nginx/html/css
COPY js /usr/share/nginx/html/js

# Copy nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Create non-root user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Give permissions to frontend files
RUN chown -R appuser:appgroup /usr/share/nginx/html

# Give nginx runtime permissions
RUN chown -R appuser:appgroup /var/cache/nginx /var/run /etc/nginx

# Switch to non-root user
USER appuser

EXPOSE 8084

# Healthcheck
HEALTHCHECK --interval=30s --timeout=5s --retries=3 \
  CMD wget --spider -q http://localhost:8084 || exit 1

CMD ["nginx", "-g", "daemon off;"]