#Install node version in dockerfile
FROM node:8.9.4-alpine

#Set work directory for dockerfile
ARG WORK_DIR=/frontend-ecommerce

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
EXPOSE 4201

#host ng serve
CMD ng serve --host 0.0.0.0