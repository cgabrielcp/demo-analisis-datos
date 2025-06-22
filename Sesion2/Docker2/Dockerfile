# -----------------------------------------------------
# Imagen base oficial de Python versión 3.9 en su variante ligera ("slim").
# Slim significa que tiene menos herramientas preinstaladas y es más liviana.
FROM python:3.9-slim

# -----------------------------------------------------
# Se define el directorio de trabajo dentro del contenedor.
# Todo el código se ubicará y ejecutará desde esta ruta.
WORKDIR /app

# -----------------------------------------------------
# Se copia el archivo requirements.txt desde el proyecto local al contenedor.
# Este archivo contiene la lista de dependencias del proyecto (librerías).
COPY requirements.txt ./

# -----------------------------------------------------
# Se instalan las dependencias especificadas en requirements.txt.
# El flag --no-cache-dir evita guardar archivos temporales para ahorrar espacio.
RUN pip install --no-cache-dir -r requirements.txt

# -----------------------------------------------------
# Se copian todos los archivos del proyecto local al directorio de trabajo en el contenedor.
COPY . .

# -----------------------------------------------------
# Se expone el puerto 5000 del contenedor, necesario si tu app Flask corre en ese puerto.
EXPOSE 5000

# -----------------------------------------------------
# Comando por defecto al ejecutar el contenedor.
# Ejecuta el archivo app.py usando Python.
CMD ["python", "app.py"]
