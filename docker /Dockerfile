# 1. Use a minimal, secure base image
FROM nginx:alpine

# 2. Remove the default nginx config (which tries to bind to port 80 as root)
RUN rm /etc/nginx/conf.d/default.conf

# 3. Copy our custom, non-root-friendly nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf

# 4. Create a non-privileged system user and group 
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# 5. Copy static files and set ownership in a single layer (best practice)
COPY --chown=appuser:appgroup . /usr/share/nginx/html

# 6. Ensure the non-root user can write to necessary nginx directories 
# (Required for temp files, logs, and cache, especially if using readOnlyRootFilesystem in K8s)
RUN chown -R appuser:appgroup /var/cache/nginx /var/run /var/log/nginx

# 7. Switch to the non-root user for the remainder of the Dockerfile and at runtime
USER appuser

# 8. Expose the non-privileged port
EXPOSE 8080

# 9. Start nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]