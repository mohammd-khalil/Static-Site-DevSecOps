# 1. Use a minimal, secure base image
FROM nginx:alpine

# 2. Create a non-privileged system user and group FIRST
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# 3. Remove the default nginx config (which tries to bind to port 80 as root)
RUN rm -f /etc/nginx/conf.d/default.conf

# 4. Copy custom nginx config (use /etc/nginx/nginx.conf if it has events/http blocks,
#    OR /etc/nginx/conf.d/default.conf if it only has a server {} block)
COPY --chown=appuser:appgroup nginx/nginx.conf /etc/nginx/conf.d/default.conf

# 5. Copy the static web pages and set ownership in a single layer
COPY --chown=appuser:appgroup ./web-page /usr/share/nginx/html/

# 6. Ensure the non-root user can write to /run (for nginx.pid), cache, logs, and conf.d
RUN chown -R appuser:appgroup /var/cache/nginx /run /var/log/nginx /etc/nginx/conf.d

# 7. Switch to the non-root user for the remainder of the Dockerfile and at runtime
USER appuser

# 8. Expose the non-privileged port
EXPOSE 8080

# 9. Start nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]
