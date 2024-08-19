# Select the base image to run the app
# We want to run JS file, so we can use Node runtime from the dockerhub
FROM node:20-alpine

# We want to set our directory for '/app' -> This is the directory where commands will be run
WORKDIR /app

COPY . . 
# Above will copy everything from our current directory to the docker image
# First dot = current directory on our machine
# Second dot = path to the current directory within the container

# Specify the command to run the app
CMD node hello.js
# Using above command -> it gave me a warning:  JSON arguments recommended for CMD to prevent unintended behavior related to OS signals
# Solution: CMD ["node", "hello.js"]