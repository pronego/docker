FROM nginx:latest

MAINTAINER Dr. Manuel Lamotte-Schubert <mls@pronego.com>

# copy local files into image
ADD nginx.conf /etc/nginx/
ADD contao.conf /etc/nginx/sites-available/

RUN mkdir /etc/nginx/sites-enabled \
 && ln -s /etc/nginx/sites-available/contao.conf /etc/nginx/sites-enabled/contao \
 && rm /etc/nginx/conf.d/default.conf

#RUN echo "upstream php-upstream { server php:9000; }" > /etc/nginx/conf.d/upstream.conf

RUN usermod -u 1000 www-data

CMD ["nginx"]

EXPOSE 80
EXPOSE 443