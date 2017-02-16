FROM node:latest

EXPOSE 11014

VOLUME /root/app/lair
WORKDIR /root/app/lair

RUN curl https://install.meteor.com/ | sh

COPY ./package.json /root/app/lair/package.json

ENV ROOT_URL=http://0.0.0.0
ENV PORT 11014
ENV MONGO_URL=mongodb://lairdb:27017/lair
ENV MONGO_OPLOG_URL=mongodb://lairdb:27017/local

CMD sleep 4 && cd /root/app/lair && meteor npm install --save babel-runtime && meteor --allow-superuser --port 11014
