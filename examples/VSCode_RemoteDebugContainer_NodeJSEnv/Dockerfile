FROM node:4.2.3
ARG http_proxy=http://10.12.1.236:8083/
ARG https_proxy=http://10.12.1.236:8083/

EXPOSE 3000
EXPOSE 5858
COPY  . /app
WORKDIR /app

RUN cd /app; npm init; npm install express --save
CMD ["node","--debug=5858","index.js"]
