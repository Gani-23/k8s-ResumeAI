# Use the official Node.js image as the base image
FROM node:20

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json first to leverage caching
COPY package*.json ./

# Install global dependencies first
RUN npm install -g -f chromium typescript

# Install local dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the application
RUN npm run build

# Expose the port that the app will run on
EXPOSE 4292

# Start the application
CMD ["npm", "start"]
