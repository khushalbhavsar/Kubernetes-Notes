FROM node:18-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "src/index.js"]

# This Dockerfile sets up a Node.js application using the official Node.js 18 Alpine image. It copies the application files, installs dependencies, exposes port 3000, and starts the application using the npm start command.
# To build the Docker image, use:
# docker build -t my-node-app .
# To run the Docker container, use:
# docker run -p 3000:3000 my-node-app
# To test the application, open your browser and navigate to http://localhost:3000
# or use curl:
# curl http://localhost:3000
# Replace "my-node-app" with your desired image name.
