# 1. Definir argumento para la versión de Ubuntu (por defecto 22.04)
ARG UBUNTU_VERSION=22.04

# 2. Usar la imagen base de Ubuntu con la versión indicada
FROM ubuntu:${UBUNTU_VERSION}

# 3. Añadir metadata con LABELS para mantener info sobre la imagen
LABEL maintainer="Oscar Astua"
LABEL version="1.0"
LABEL description="Imagen Ubuntu con Nginx y variables de entorno definidas"

# 4. Actualizar apt e instalar nginx sin interacción
RUN apt-get update && apt-get install -y nginx && apt-get clean

# 5. Crear directorio personalizado para el sitio web
RUN mkdir -p /var/www/mi_carpeta_para_index

# 6. Copiar archivo index.html personalizado al directorio creado
COPY index.html /var/www/mi_carpeta_para_index/index.html

# 7. Reemplazar el directorio default de nginx con enlace simbólico al nuevo (nginx servidor web)
RUN rm -rf /var/www/html && ln -s /var/www/mi_carpeta_para_index /var/www/html

# 8. Exponer el puerto 80 para documentar el puerto HTTP del contenedor (IMPORTANTE: Esto no expone el puerto, unicamente lo documenta)
EXPOSE 80

# 9. Definir variables de entorno que estarán disponibles en el contenedor
ENV CREATOR="Dios"
ENV APP_ENVIROMENT=PRODUCTION

# 10. Definir ENTRYPOINT para nginx
ENTRYPOINT ["nginx"]

# 11. CMD con argumentos por defecto para que nginx corra en primer plano
CMD ["-g", "daemon off;"]
