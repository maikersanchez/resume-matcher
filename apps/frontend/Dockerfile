# Use la imagen base de Node.js
FROM node:18-alpine

# Establecer el directorio de trabajo
WORKDIR /app

# Paso de depuración: Mostrar el directorio actual, debería estar vacío.
RUN echo "--- PASO 1: DIRECTORIO DE TRABAJO ---" && ls -la

# Copiar package.json y package-lock.json
# Esto es crucial para que npm install funcione.
COPY package*.json ./

# Paso de depuración: Comprobar si los archivos package.json se copiaron correctamente.
RUN echo "--- PASO 2: DESPUÉS DE COPIAR package.json ---" && ls -la

# Instalar las dependencias
# Esto solo se ejecutará si package.json fue copiado.
RUN npm install

# Paso de depuración: Comprobar los archivos después de la instalación de dependencias.
# Deberías ver la carpeta node_modules aquí.
RUN echo "--- PASO 3: DESPUÉS DE npm install ---" && ls -la

# Copiar todo el código fuente de la aplicación
# La instrucción 'COPY . .' copiará los archivos de tu contexto de construcción.
COPY . .

# Paso de depuración: Mostrar todos los archivos de la aplicación.
# Deberías ver todo tu código (incluyendo la carpeta `app`).
RUN echo "--- PASO 4: DESPUÉS DE COPIAR EL CÓDIGO FUENTE ---" && ls -la

# Configurar variables de entorno
ENV NODE_ENV=development
ENV NEXT_TELEMETRY_DISABLED=1

# Exponer el puerto
EXPOSE 3000

# Comando para iniciar la aplicación
CMD ["npm", "run", "dev"]
