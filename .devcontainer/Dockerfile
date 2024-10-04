FROM mcr.microsoft.com/vscode/devcontainers/base:ubuntu

# use this Dockerfile to install additional tools you might need, e.g.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>
# Use base image

# Avoid prompts during installations
ENV DEBIAN_FRONTEND=noninteractive

# Install Node.js, MongoDB, and other necessary tools
RUN apt-get update && apt-get install -y \
    nodejs \
    npm \
    mongodb \
    curl

# Install pnpm globally
RUN npm install -g pnpm

# Set up MongoDB data directory
RUN mkdir -p /data/db

# Start MongoDB service
RUN service mongodb start

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Expose ports (e.g., 3000 for Node.js app, 27017 for MongoDB)
EXPOSE 3000 27017

# Set the working directory for the application
WORKDIR /workspace

# Copy project files (add a .dockerignore file to avoid copying node_modules)
COPY . .

# Install dependencies using pnpm
RUN pnpm install

# Start the Node.js application
CMD ["pnpm", "start"]
