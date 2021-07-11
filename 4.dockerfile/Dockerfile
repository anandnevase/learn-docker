FROM nginx:alpine
LABEL maintainer="anandnevase"
COPY index.html /usr/share/nginx/html/
EXPOSE 80
ENTRYPOINT ["nginx", "-g", "daemon off;"]