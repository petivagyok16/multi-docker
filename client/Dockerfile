# builder phase from node alpine
FROM node:alpine as builder

# specifying the work directory
WORKDIR '/app'
# copying package.json from root and installing it
COPY package.json .
RUN npm install

# after install finished copying all our source files from root to /app and building them
COPY . .
RUN npm run build


# run phase - dumping everything from the previous step and copying only we need
# nginx will take care the rest
FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html
