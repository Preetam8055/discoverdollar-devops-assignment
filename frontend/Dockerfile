# Build Angular app
FROM node:18 AS build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

RUN npm run build -- --configuration production

# Serve using nginx
FROM nginx:alpine

# remove default nginx page
RUN rm -rf /usr/share/nginx/html/*

# copy angular build output
COPY --from=build /app/dist/* /usr/share/nginx/html/

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]