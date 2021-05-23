FROM node:16

ENV APP_ROOT=/app APP_PORT=3000
ENV BGG_DB_HOST=localhost BGG_DB_PORT=3306 BGG_DB_USER=root BGG_DB_PASSWORD=changeit

## build image
WORKDIR ${APP_ROOT}

ADD main.js .
ADD package.json .
ADD package-lock.json .

ADD bootstrap_public bootstrap_public
ADD bootstrap_views bootstrap_views
ADD lib lib
ADD public public
ADD views views

RUN npm i

## run image
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
	CMD curl -s -f http://localhost:${APP_PORT}/health || exit 1

EXPOSE ${APP_PORT}

ENTRYPOINT [ "node", "main.js", "--html" ]
