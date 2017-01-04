FROM node:4.2.3
# Haufe Group Proxy server settings comment out if you are not behind the firewall.
ARG http_proxy=http://10.12.1.236:8083/
ARG https_proxy=http://10.12.1.236:8083/
# Run the app on port 3000 of the host machine
EXPOSE 3000
# Open port 5858 to hook up remote debugging
EXPOSE 5858
COPY  . /app
WORKDIR /app
# Initialize npm and create package.json, install express "persistant"
RUN cd /app; npm init; npm install express --save
#Configure node to use its debugger utility on index.js app
CMD ["node","--debug=5858","index.js"]
