# this shows how we can extend/change an existing official image from Docker Hub

FROM nginx:latest

# change working directory to root of nginx webhost
# using WORKDIR is preferred to using 'RUN cd /some/path'
WORKDIR /usr/share/nginx/html

COPY index.html index.html

# I don't have to specify EXPOSE or CMD because they're in my FROM