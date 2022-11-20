FROM node:19-alpine 
LABEL maintainer="nuance.com"

RUN mkdir /app 

# Installing git & clone postman-exorter repository
RUN apk update \ 
 && apk add git \
 && git clone -b v0.1.3 https://github.com/hudeldudel/postman-exporter.git /app \
 && npm install -g newman

# Working directory as "/postman-exporter"
WORKDIR /app

# Removing default config files
RUN rm -rf config/* && sed "/app.listen.* /i app.use('/static/svc-config-files/',express.static('/app/audio-files/'))" -i /app/main.js

# copy modified config files 
COPY  config/* ./config/
COPY ./audio-files/* ./audio-files/

# Installing dependency
RUN npm install && npm cache clean --force --loglevel=error

# start the app
CMD [ "npm", "start"]

