# OPCIÓN C: Si usas el build context correcto en Coolify
# (Build Context: ./frontend en Coolify)
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "run", "dev"]
