FROM nginx:1.21.5-alpine

# Set maintainer label
LABEL maintainer="Arif Ginanjar <arif17ginanjar@gmail.com>"

# Set Buold Arg
ARG APP_REPOSITORY=https://github.com/milicodes/weather-app-page.git

# Install git
RUN apk add --no-cache git

# Set timezone to jakarta
RUN apk add tzdata \
    && cp /usr/share/zoneinfo/Asia/Jakarta /etc/localtime \
    && echo "Asia/Jakarta" >  /etc/timezone \
    && apk del tzdata

# Clean up and set workdir
RUN rm -rf /usr/share/nginx/html/*
WORKDIR /usr/share/nginx/html

# Clone App to Workdir
RUN git clone ${APP_REPOSITORY} .
COPY ./dependencies/nginx/nginx.conf /etc/nginx/conf.d/default.conf

#run build
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]