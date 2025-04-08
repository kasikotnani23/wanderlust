# stage 1: build the app
# use the official node image as a base image
FROM node:21 as backend-builder
# set the working directory in the container
WORKDIR /app
# copy the package.json and package-lock.json files to the working directory
COPY package*.json ./
# install the dependencies
RUN npm install
# copy the rest of the application code to the working directory
COPY . .
#Npm Run the tests
RUN npm run test
 
# stage 2: run the app

# use a smaller image for the final stage
FROM node:21-alpine
# workdir for the app
WORKDIR /app
# copy the node_modules and build from the builder stage
COPY --from=backend-builder app/ .
# copy the environment variables file
COPY  .env.sample .env
# port to expose
EXPOSE 5000
# run the app
CMD ["npm", "start"]
