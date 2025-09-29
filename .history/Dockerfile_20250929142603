# Use nginx alpine image for a lightweight container
FROM nginx:alpine

# Copy the HTML file to nginx's default html directory
COPY index.html /usr/share/nginx/html/

# Copy custom nginx configuration
COPY nginx.conf /etc/nginx/nginx.conf

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
