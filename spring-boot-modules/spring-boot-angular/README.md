## Composing docker file with frontend and backend container's in yml file.

To run docker compose file use below commands.

1. docker-compose up --build ( To install all dependencies from dockerfile and run application on container).

* A container is well orchestrated to host an application in server with mircoservices, which runs in small parts.
* A dockerfile consist of microservices which helps to reduce application design and expose an API.
* A dockerfile consist of images with full of packages and dependencies which run on application.
* After completing dockerfile the below commands are used to create an image and container.
  1. docker build -t <image> . ( build a particular image in current directory with .)
  2. docker images ( To check images in container)
  3. docker run -p 4200:4200 <container name> <image name> ( the build image will run on container with specified port number.)
  4. Test your application with http://localhost:4200/users to browse.
  
## Below is the dockerfile that contains instructions on building a docker image.
  
#Install node version image in dockerfile
FROM node:8.9.4-alpine

#Set work directory for dockerfile
ARG WORK_DIR=/frontend-application

#Add enivormental variable to add modules in /bin, which is useful to run ng serve.
ENV PATH ${WORK_DIR}/node_modules/.bin:$PATH

#For making root to frontend and set work directory.
RUN mkdir ${WORK_DIR}
WORKDIR ${WORK_DIR}

#Copying packages files from local to container.
COPY package.json ${WORK_DIR}
COPY package-lock.json ${WORK_DIR}

#Installing npm to install dependencies.
RUN npm install

#Run ng build for production.
RUN npm run build --prod

#Copying wrk_dir after npm to update only the source files instead of depndencies.
COPY . ${WORK_DIR}

#Expose port for angular
EXPOSE 80

#host ng serve
CMD ng serve --host 0.0.0.0
