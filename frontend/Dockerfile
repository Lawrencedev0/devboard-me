FROM node:20 AS build
 
WORKDIR /app

COPY package*.json ./

RUN npm ci

COPY . . 

RUN npm run build

FROM node:20-alpine AS runner

WORKDIR /app

RUN npm install -g vite@5 && npm cache clean --force

COPY --from=build /app/dist ./dist

COPY vite.preview.config.js ./vite.config.js

EXPOSE 4173

CMD ["vite", "preview", "--host", "0.0.0.0", "--port", "4173"]
