FROM node:20-alpine

WORKDIR /app

COPY frontend/ /app

RUN npm install && npm run build

# Serve via simple HTTP server (you can use nginx if needed)
RUN npm install -g serve

CMD ["serve", "-s", "dist", "-l", "3000"]
