FROM node:18.17.0 AS build

WORKDIR /app
COPY . .

ENV REACT_APP_BACKEND_URL api

RUN corepack enable
RUN npm install

RUN yarn build

FROM nginx:alpine

COPY --from=build /app/build /usr/share/nginx/html
COPY default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
