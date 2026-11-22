FROM nginx:alpine

# 1. Create non-root user and group
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# 2. Remove default config
RUN rm -f /etc/nginx/conf.d/default.conf

# 3. Keep root:root ownership on config & static files, and grant read-only permissions (644/755)
COPY --chown=root:root --chmod=644 nginx/nginx.conf /etc/nginx/conf.d/default.conf
COPY --chown=root:root --chmod=755 ./web-page /usr/share/nginx/html/

# 4. Only grant appuser write access to runtime directories (PID, cache, logs)
RUN chown -R appuser:appgroup /var/cache/nginx /run /var/log/nginx

# 5. Switch to non-root user
USER appuser

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
