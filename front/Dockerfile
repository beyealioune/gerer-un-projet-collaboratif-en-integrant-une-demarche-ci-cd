# Use an official Node.js runtime as a parent image
FROM node:16

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY front/package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY front/ .

# Build the application
RUN npm run build

# Set environment variables (if needed)
ENV NODE_ENV=production

# Expose port (if needed)
EXPOSE 3000

# Command to run the application
CMD ["npm", "start"]
