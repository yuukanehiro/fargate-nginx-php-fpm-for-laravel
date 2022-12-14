FROM nginx:latest

ARG ENVIRONMENT="local" // override by CI/CD! ["develop"|"staging"|"production"]
ARG PHP_FPM_CONTAINER_WWW_DATA_USER_ID=82
ARG PHP_FPM_CONTAINER_WWW_DATA_GROUP_ID=82

# デバッグ用curl
RUN if [ "${ENVIRONMENT}" = "develop" -o "${ENVIRONMENT}" = "staging" ]; then \
        apt-get install -y curl; \
fi
RUN apt-get -y update && apt-get clean


RUN usermod -u ${PHP_FPM_CONTAINER_WWW_DATA_USER_ID} www-data && \
    groupmod -g ${PHP_FPM_CONTAINER_WWW_DATA_GROUP_ID} www-data

COPY ./ecs/environments/${ENVIRONMENT}/docker/nginx/conf.d /etc/nginx/conf.d
COPY ./ecs/environments/${ENVIRONMENT}/docker/nginx/conf/nginx.conf /etc/nginx/nginx.conf
RUN nginx -t

RUN mkdir -p /var/www/app/public
COPY ./src/public /var/www/app/public
WORKDIR /var/www/app/public
RUN chown -R www-data:www-data /var/www/app

ENTRYPOINT ["nginx", "-g", "daemon off;"]
EXPOSE 80
