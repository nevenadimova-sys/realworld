# ---- Build stage ----
FROM node:10-alpine AS builder
WORKDIR /app

COPY package.json ./
RUN npm install

COPY . .

ARG REACT_APP_API_ROOT
ENV REACT_APP_API_ROOT=$REACT_APP_API_ROOT

RUN npm run build

# ---- Runtime stage ----
FROM nginx:alpine
COPY --from=builder /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
