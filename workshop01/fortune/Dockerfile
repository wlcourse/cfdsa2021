# pull base image with tag
# use node version 16 image
From node:16

# define environment variables
ENV APP_ROOT=/app APP_PORT=3000

## START build image

# create /app directory and cd into /app
WORKDIR ${APP_ROOT}

# inside APP_ROOT
# copy files into directory APP_ROOT
ADD main.js .
ADD package.json .
ADD package-lock.json .
# create directories and copy files in created directories
# cannot use "." as it will only copy files inside directory without creating directory
ADD public public
ADD views views

# install the packages in package.json
RUN npm install

## END build image

## START run image

# add healthcheck
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
	CMD curl -s -f http://localhost:${APP_PORT}/healthz || exit 1

# container listens on port 3000 based on application code
EXPOSE ${APP_PORT}

# run application using node
ENTRYPOINT ["node", "main.js"]

## END run image
