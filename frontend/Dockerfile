FROM node:18 as build

WORKDIR /app

ENV REACT_APP_BACKEND_URL api

RUN git clone --depth 1 https://github.com/fams/guess_game.git . &&\
    cd frontend &&\
    npm install &&\
    npm run build


FROM nginx:latest

COPY nginx.conf /etc/nginx/conf.d/default.conf

RUN rm -rf /usr/share/nginx/html/*

COPY --from=build /app/frontend/build /usr/share/nginx/html/

ENTRYPOINT ["nginx", "-g", "daemon off;"]