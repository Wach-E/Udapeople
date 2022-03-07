FROM node:14
ENV NODE_ENV production
# Add a work directory
WORKDIR /app
# Copy app files
COPY dist/ .
# Install serve
RUN npm install serve -g 
# Expose port
EXPOSE 3000
# Start serve
CMD ["serve", "-s", "dist"]