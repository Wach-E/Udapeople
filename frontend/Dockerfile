FROM node:16.13.2
ENV NODE_ENV production
# Add a work directory
WORKDIR /app
# Install webpack-cli globally
RUN npm install webpack-cli -g
# Cache and Install dependencies
COPY package*.json ./
# Install app dependencies
RUN npm install
# Copy app files
COPY . .
# Build the app
RUN npm run build -y
# Install serve
RUN npm install serve -g 
# Expose port
EXPOSE 3000
# Start serve
CMD ["serve", "-s", "dist"]