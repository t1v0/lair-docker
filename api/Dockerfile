FROM golang:latest

EXPOSE 11015

RUN git clone https://github.com/lair-framework/api-server

RUN cd api-server \
 && git fetch origin refs/pull/8/head:pr/8 \
 && git checkout pr/8 \
 && go install -v

ENV MONGO_URL=mongodb://lairdb:27017/lair
ENV API_LISTENER=0.0.0.0:11015

CMD api-server
