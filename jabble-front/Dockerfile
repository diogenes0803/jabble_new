# Base image
FROM node:20 AS base
WORKDIR /app
COPY package*.json ./

# Install dependencies for production
FROM base AS production
RUN npm install --only=production
RUN npm run build
EXPOSE 3000
CMD ["npm", "start"]

# Install dependencies for development
FROM base AS development
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "run", "dev"]
