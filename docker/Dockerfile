FROM node:latest

RUN apt-get update && apt-get -y upgrade

RUN apt-get install apt-transport-https

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
      && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
      && apt-get update && apt-get -y install yarn

# Fix bug https://github.com/npm/npm/issues/9863
RUN cd $(npm root -g)/npm \
      && npm install fs-extra \
      && sed -i -e s/graceful-fs/fs-extra/ -e s/fs\.rename/fs.move/ ./lib/utils/rename.js

WORKDIR /app
RUN npm install
