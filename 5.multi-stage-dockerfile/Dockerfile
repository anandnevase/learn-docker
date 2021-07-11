FROM alpine AS stage1
 LABEL maintainer="anandnevase"
 RUN echo "Welcome to Docker Labs!" > /opt/index.html

FROM nginx:alpine
LABEL maintainer="Collabnix"
COPY --from=stage1 /opt/index.html /usr/share/nginx/html/
ENTRYPOINT ["nginx", "-g", "daemon off;"]