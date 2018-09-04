#docker build -t snowsprout/node-pm2 .

FROM node:8.11.3

# Install PM2
RUN npm install -g pm2
WORKDIR /usr/src/apps

CMD ["pm2-docker", "process.yml"]
