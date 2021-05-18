FROM node:16

ENV APP_ROOT=/app APP_PORT=3000 BGG_DB_HOST=localhost BGG_DB_PORT=3000 BGG_DB_USER=root BGG_DB_PASSWORD=mypassword

# create the /app dir and cd into /app
WORKDIR ${APP_ROOT}

# we are now inside APP_ROOT
# copy the following files and directories. "." represents current directory
ADD main.js .
ADD package-lock.json .
ADD package.json .

ADD bootstrap_public bootstrap_public
ADD bootstrap_views bootstrap_views
ADD lib lib
ADD public public
ADD views views

# install the packages in package.json
RUN npm install
RUN npm i

# run the application
ENTRYPOINT [ "node", "main.js" ]
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
    cmd curl -s -f http://localhost:${APP_PORT}/health || exit 1

EXPOSE ${APP_PORT}

ENTRYPOINT ["node", "main.js"]