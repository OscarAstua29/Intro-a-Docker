# 1. Definimos la imagen base, en este caso Python 3.10 ligera
FROM python:3.10-slim

# 2. Establecemos el directorio de trabajo dentro del contenedor(como hacer un cd)
WORKDIR /app

# 3. Actualizamos pip
RUN python -m pip install --upgrade pip

# 4. Creamos LABELS
LABEL maintainer="Oscar Astua"
LABEL description="Calculadora interactiva en Python. Ejecutar con: docker run -it calcu"

# 5. Copiamos el script Python que queremos ejecutar
COPY calculadora.py .

# 6. Comando que se ejecuta al iniciar el contenedor
CMD ["python", "calculadora.py"]
