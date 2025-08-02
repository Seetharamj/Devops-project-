# Use official Node.js base image
FROM node:14

# Create app directory
WORKDIR /usr/src/app

# Copy app files
COPY package*.json ./
RUN npm install

COPY . .

# Expose port
EXPOSE 3000

# Command to run the app
CMD [ "node", "app.js" ]
