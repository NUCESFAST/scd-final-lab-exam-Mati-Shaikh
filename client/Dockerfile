# Use the official Node.js image as the base image
FROM node:14

# Set the working directory
WORKDIR /your_1222_frontend

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application
COPY . .

# Build the frontend assets
RUN npm run build

# Expose the frontend port
EXPOSE 1222

# Start the frontend application
CMD ["npm", "start"]
