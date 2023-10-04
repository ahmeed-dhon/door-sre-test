FROM node:18-alpine

LABEL Name="nodejs-service" \
      Version="1.0"

WORKDIR /usr/src/app

COPY . .

# Service and Management ports
EXPOSE 5000/tcp

CMD [ "node", "server.js" ]