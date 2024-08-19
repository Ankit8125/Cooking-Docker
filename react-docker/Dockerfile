# Hover for more info

# set the base image to create the image for react app
# 20 - version of node, we can use any version of the node
FROM node:20-alpine
# Hover for more info
# => FROM node:20-alpine: This line sets the base image for the Docker image. It uses Node.js version 20 on an Alpine Linux distribution, which is a lightweight version of Linux.

# To protect our container from users who are wanting to do something bad with it, we create a new user with permissions only to run the app 
# create a user with permissions to run the app
# -S -> create a system user
# -G -> add the user to a group
# This is done to avoid running the app as root user (root user - that has access to everything)
# If the app is run as root, any vulnerability in the app can be exploited to gain access to the host system
# It's a good practice to run the app as a non-root user
RUN addgroup app && adduser -S -G app app
# Hover for more info
# Reason: If our system is hacked and suppose we are using it as root user, then obviously the attacker can mess up our work. That's why it's preferred to use it as non-root user
# => This command creates a new user group named app and a new system user named app that belongs to this group. This is done to avoid running the application as the root user, which is a security best practice.

# set the user to run the app
USER app
# Hover for more info
# => This sets the default user for the following instructions to the app user created earlier.

# set the working directory to /app
WORKDIR /app
# Hover for more info
# => This sets the working directory inside the container to /app. All subsequent commands will be run in this directory.

# copy package.json and package-lock.json to the working directory
# This is done before copying the rest of the files to take advantage of Docker’s cache
# If the package.json and package-lock.json files haven’t changed, Docker will use the cached dependencies
COPY package*.json ./
# Hover for more info
# => This copies package.json and package-lock.json files from the host machine to the working directory in the container. This is done to leverage Docker's caching mechanism, which speeds up the build process if dependencies haven't changed.

# sometimes the ownership of the files in the working directory is changed to root
# and thus the app can't access the files and throws an error -> EACCES: permission denied
# to avoid this, change the ownership of the files to the root user
USER root
# Hover for more info
# => Temporarily switches back to the root user to change file ownership (which is necessary because only the root user has the permissions required to change ownership of files.)

# change the ownership of the /app directory to the app user
# chown -R <user>:<group> <directory>
# chown command changes the user and/or group ownership of for given file.
RUN chown -R app:app .
# Hover for more info
# => By running this command, you ensure that the app user, which will run the application, has full control over the files in the /app directory.

# change the user back to the app user
USER app
# Hover for more info
# => After changing the ownership, you switch back to the app user to ensure that the rest of the commands (like npm install and running the application) are executed with the limited permissions of the app user.

# install dependencies
RUN npm install
# Hover for more info
# => Installs the Node.js dependencies defined in package.json.

# copy the rest of the files to the working directory
COPY . .
# Hover for more info
# => Copies all remaining files from the host machine to the working directory in the container.

# expose port 5173 to tell Docker that the container listens on the specified network ports at runtime
EXPOSE 5173
# Hover for more info
# => Informs Docker that the container will listen on port 5173 at runtime. This is typically the port your React development server runs on.

# command to run the app
CMD npm run dev
# Hover for more info
# => Specifies the command to run when the container starts. In this case, it runs the development server for the React application.