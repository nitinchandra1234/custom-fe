# Use an official Node runtime as the base image
FROM node:14

# Set the working directory in the container to /app
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install any needed packages specified in package.json
RUN npm install

# Bundle app source inside Docker image (by copying from your machine’s local context into the container)
COPY . .

# Make port 300 available to the world outside this container
EXPOSE 3000

# Run the app when the container launches
CMD ["npm", "start"]
