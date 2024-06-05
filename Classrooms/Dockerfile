# Use the official Node.js image as the base image
FROM node:14

# Set the working directory
WORKDIR /your_1222_backend

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application
COPY . .

# Expose the backend port
EXPOSE 3222

# Start the backend application
CMD ["node", "index.js"]
