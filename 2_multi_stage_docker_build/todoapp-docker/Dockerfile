FROM node:18-alpine AS build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:alpine AS deploy
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

# To build the Docker image, run:
# docker build -t khushalbhavsar/todoapp:latest .
# To run the Docker container, run:
# docker run -p 8080:80 khushalbhavsar/todoapp:latest
# Then access the application at http://localhost:8080
# RUN npm install --production
# To push the image to Docker Hub, use:
# docker tag todoapp:latest khushalbhavsar/todoapp:latest
# docker push khushalbhavsar/todoapp:latest

