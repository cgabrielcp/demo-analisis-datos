# -----------------------------------------------------
# Se define la imagen base: Ubuntu versión 20.04 LTS.
# Esta imagen es estable, ampliamente usada en servidores
# y sirve como base limpia para construir nuestro entorno.
FROM ubuntu:20.04

# -----------------------------------------------------
# Esta variable de entorno evita que el sistema operativo
# solicite interacciones manuales (como zonas horarias)
# durante la instalación de paquetes con apt.
ENV DEBIAN_FRONTEND=noninteractive

# -----------------------------------------------------
# Se actualiza el sistema y se instalan los siguientes paquetes:
# - python3: intérprete de Python
# - python3-pip: gestor de paquetes de Python
# - python3-dev: cabeceras de Python para compilar librerías
# - build-essential: herramientas de compilación como gcc, make
# - wget: para descargar archivos desde internet
# Luego se limpia la cache para reducir el tamaño de la imagen.
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    python3-dev \
    build-essential \
    wget && \
    apt-get clean

# -----------------------------------------------------
# Se actualiza pip y se instala Jupyter Notebook,
# que será el entorno interactivo principal que usaremos.
RUN pip3 install --upgrade pip && \
    pip3 install notebook==6.5.6

# -----------------------------------------------------
# Se define el directorio de trabajo dentro del contenedor.
# Todo el código y archivos se manejarán desde aquí por defecto.
WORKDIR /workspace

# -----------------------------------------------------
# Se crea el directorio donde se guardarán las configuraciones
# del usuario root para Jupyter.
RUN mkdir -p /root/.jupyter

# -----------------------------------------------------
# Se agregan configuraciones básicas al archivo de configuración
# de Jupyter Notebook para:
# - deshabilitar la autenticación por token y contraseña
# - permitir su uso como root
# - evitar que se abra el navegador automáticamente
RUN echo "c.NotebookApp.token = ''" >> /root/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.password = ''" >> /root/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.open_browser = False" >> /root/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.allow_root = True" >> /root/.jupyter/jupyter_notebook_config.py

# -----------------------------------------------------
# Se expone el puerto 8888, que es el puerto por defecto de Jupyter.
# Esto permite acceder al notebook desde el navegador en el host.
EXPOSE 8888

# -----------------------------------------------------
# Comando por defecto al iniciar el contenedor:
# Lanza Jupyter Notebook accesible desde cualquier IP
# en el puerto 8888, sin abrir navegador, y como root.
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]
