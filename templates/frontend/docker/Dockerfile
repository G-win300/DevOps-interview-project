# stage 1
FROM node:14-alpine as build-stage
    
RUN npm install -g @vue/cli 
  
ENV NODE_OPTIONS="--max-old-space-size=8192"
ADD package.json package-lock.json* /source/
WORKDIR /source
RUN npm install
ADD . /source
WORKDIR /source
RUN npm install && cp .env.k8s .env && npm run build

# stage 2
FROM nginx:stable-alpine as production-stage
ADD docker/default.conf /etc/nginx/conf.d/default.conf
COPY --from=build-stage /source/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]