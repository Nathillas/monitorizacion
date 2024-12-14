# Herramientas propias del sistema

Los sistemas operativos y plataformas modernas incluyen herramientas integradas para la monitorización básica. Estas herramientas ofrecen métricas esenciales como uso de CPU, memoria, disco y red.


## Indice

[1. Procesos](https://github.com/Nathillas/monitorizacion/edit/main/herramientas.md#1procesos)  

[2. Red](https://github.com/Nathillas/monitorizacion/edit/main/herramientas.md#2monitorizaci%C3%B3n-de-red)  

[3. Archivos y Recursos](https://github.com/Nathillas/monitorizacion/edit/main/herramientas.md#3gesti%C3%B3n-de-sistemas-de-archivos-y-recursos)

  

### **1.Procesos**

### **`ps`**
El comando `ps` permite mostrar información sobre los procesos en ejecución.

- `ps a`: Muestra todos los procesos asociados a un terminal.  
  Uso: Identificar los procesos que están ejecutándose en sesiones de terminal activas.

![imagen](/img/imagen1.png)

- `ps au`: Proporciona información detallada sobre los procesos.  
  Uso: Obtener detalles adicionales, como el usuario, consumo de CPU y memoria.

![imagen](/img/imagen2.png)

- `ps aux`: Lista todos los procesos en ejecución en el sistema.  
  Uso: Mostrar información de todos los procesos, incluso aquellos no vinculados a un terminal.

![imagen](/img/imagen3.png)


- `ps -C [proceso]`: Busca información de un proceso específico por su nombre.  
  Uso: Identificar un proceso concreto.

![imagen](/img/imagen4.png)

Para ver 5 los procesos que ocupen más memoria:
~~~
 ps -eo user,pid,%cpu,%mem,time --sort=-%cpu | head -n 6
~~~

![imagen](/img/imagen5.png)


---

### **`top`**
Muestra los procesos del sistema ordenados por consumo de CPU en tiempo real.

- Por defecto: Muestra los procesos activos ordenados por CPU.  
  Uso: Identificar los procesos que más recursos están consumiendo.

![imagen](/img/imagen6.png)

- Crear registro: Guarda la salida de `top` en un archivo de texto.  
  Uso: Generar un registro para su análisis posterior.

  ~~~
  top > top.txt
  ~~~  
![imagen](/img/imagen7.png)

- 10 procesos que más CPU consumen por periodos de 3 segundos

![imagen](/img/imagen8.png)

---

### **`htop`**
Una herramienta interactiva para monitorizar procesos, similar a `top` pero con una interfaz más visual.
Instalación:
~~~
sudo apt install htop
~~~

- Sin parámetros: Ejecuta el monitor interactivo.  
  Uso: Navegar fácilmente entre procesos, monitorear recursos y finalizar tareas.
![imagen](/img/imagen9.png)

---

### **`atop`**
Herramienta avanzada para monitorizar el rendimiento del sistema y de los procesos.
![imagen](/img/imagen10.png)

- Configuración: Modificar el archivo `/etc/default/atop` para cambiar el intervalo de registro.  
  Parámetro: Cambiar `LOGINTERVAL=600` a `LOGINTERVAL=60` para reducir el intervalo a 1 minuto.
![imagen](/img/imagen11.png)

- Leer registros: Reproducir un archivo de registro generado.  
~~~
   atop -r nombre_archivo  
~~~
Uso: Analizar el rendimiento histórico del sistema.
![imagen](/img/imagen12.png)

---

### **Finalizar un Proceso**
Permite identificar y detener procesos.

- Identificar procesos: Utilizar `ps au` para listar los procesos con sus respectivos PID.  

- Matar un proceso: Utilizar `kill -9 [PID]` para finalizar un proceso de manera forzada.  
  Ejemplo:
  ~~~
  kill -9 12345
  ~~~


  

---

## **2.Monitorización de Red**

### **`tcpdump`**
Herramienta para capturar y analizar paquetes de red.
![imagen](/img/imagen21.png)


- Para capturar el tráfico de red en una interfaz específica.
  ~~~
  tcpdump -i [interfaz]
  ~~~
- Para guardar la salida de tcpdump en un archivo, puedes redirigir la salida a un archivo de texto.
  ~~~
  sudo tcpdump -i eth0 -w capturas
  ~~~

![imagen](/img/imagen23.png)

- Leer un archivo de captura: Utilizar `tcpdump -r [archivo]` para analizar capturas guardadas previamente.  
  
  ~~~
  tcpdump -r capturas
  ~~~

---

### **`tcptrack`**
Monitorea las conexiones TCP activas en tiempo real.
~~~
tcptrack -i [interfaz]
~~~
  Uso: Visualizar conexiones TCP activas en una interfaz específica.
![imagen](/img/imagen24.png)

---

### **`iptraf-ng`**
Monitoriza estadísticas de tráfico de red en tiempo real.
~~~
iptraf
~~~

  Uso: Inicia la interfaz interactiva para monitorear estadísticas de tráfico.
![imagen](/img/imagen27.png)

---

### **`bmon`**
Proporciona una visualización en tiempo real del uso de ancho de banda.
~~~
bmon
~~~
 
  Uso: Inicia el monitor interactivo de ancho de banda.
![imagen](/img/imagen26.png)

---

### **`du`**
Permite calcular el tamaño de un archivo.
~~~
du -hs [archivo]
~~~
  Uso: Muestra el tamaño del archivo en formato legible.

---

## **3.Gestión de Sistemas de Archivos y Recursos**

### **`free`**
Muestra la cantidad de memoria libre y utilizada en el sistema.
![imagen](/img/imagen13.png)

Usando free -h, la salida se muestra en un formato más legible para el usuario
~~~
free -h
~~~

![imagen](/img/imagen14.png)

Para verlo en intervalos de 3s por ejemplo
~~~
free -s 3
~~~
![imagen](/img/imagen15.png)


### **`df`**
El comando `df` muestra información sobre el espacio disponible y utilizado en los sistemas de archivos montados.

- `-h`: Muestra tamaños en formato legible para humanos.  
- `-T`: Muestra el tipo de sistema de archivos.  
- `-i`: Muestra el uso de inodos (número de archivos).  
- `-a`: Muestra información de todos los sistemas de archivos, no solo los montados.

![imagen](/img/imagen16.png)

---

### **`du`**
La utilidad `du` se utiliza para estimar el espacio utilizado por directorios y archivos en un sistema de archivos.

- `-h`: Muestra tamaños en formato legible para humanos.  
- `-s`: Muestra solo el total de cada argumento.  
- `-c`: Muestra el total acumulado al final.  
- `-k`: Muestra tamaños en kilobytes.

![imagen](/img/imagen17.png)

- Ver cantidad de uso por usuario /home

~~~
du -h --max-depth=1 /home
~~~
![imagen](/img/imagen18.png)

---

### **`iostat`**
El comando `iostat` muestra estadísticas de entrada/salida del sistema.

- `-c`: Muestra resúmenes de CPU.  
- `-d`: Muestra resúmenes de dispositivos de bloques.  
- `-h`: Muestra tamaños en formato legible para humanos.  
- `-t`: Muestra el tiempo en cada línea.
- `-x`: Muestra información extendida sobre las estadísticas de dispositivos de E/S.

![imagen](/img/imagen19.png)

Para verlo en intervalos de 5s

![imagen](/img/imagen20.png)

---

### **`lsof`**
`lsof` (List Open Files) muestra una lista de archivos abiertos por procesos en el sistema.

- `-i`: Filtra por conexiones de red.  
- `-u`: Filtra por usuarios.  
- `-p`: Filtra por PID.  
- `-c`: Filtra por nombre de comando.

---

### **`blkid`**
El comando `blkid` muestra información sobre los dispositivos de bloque, como UUID y tipo de sistema de archivos.

- `-o`: Especifica el formato de salida (`list`, `value`, o `full`).  
- `-p`: Evita escanear particiones.

---

### **`fdisk`**
`fdisk` es una herramienta para la manipulación de tablas de particiones en discos.

- `-l`: Lista las particiones del sistema.  
- `-u`: Muestra la tabla de particiones en sectores.  
- `-p`: Muestra la tabla de particiones en formato legible.  
- `-n`: Añade una nueva partición.  
- `-d`: Elimina una partición.  
- `-t`: Cambia el tipo de una partición.  
- `-w`: Escribe la tabla de particiones en el disco.  
- `-q`: Sale sin guardar cambios.

---

