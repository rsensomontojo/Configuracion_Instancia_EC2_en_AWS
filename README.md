# Configuración de Instancia EC2 en AWS para 2DAW

## Requisitos Previos
- Cuenta en AWS
- Terminal (Linux/Mac o Windows con configuración especial)
- Archivo .pem de conexión

## Pasos de Configuración

### 1. Acceso a AWS
1. Entrar en consola AWS
2. Buscar servicio EC2
3. Marcar servicio con estrella (favoritos)

### 2. Preparación de Entorno Local
1. Crear carpeta `AWS-2DAW`
2. Guardar archivo `.pem` en esta carpeta

### 3. Configuración de Permisos de Archivo .pem
```bash
# Cambiar permisos del archivo
chmod 400 labuser.pem

# Verificar permisos
ll
```

### 4. Lanzar Instancia EC2

#### Configuración:
- **Nombre**: Identificativo para la instancia
- **AMI**: Amazon Linux 2023 (Free tier)
- **Arquitectura**: 64bit x86
- **Tipo Instancia**: t2.micro (Free tier)
- **Key Pair**: VocKey
- **Network Settings**:
  - Auto-assign Public IP: ENABLED
- **Firewall (Security Group)**: 
  - Permitir tráfico SSH desde cualquier origen
- **Almacenamiento**: 8GB GP3

### 5. Conexión SSH
```bash
# Estructura de conexión
ssh -i labuser.pem ec2-user@[IP_PUBLICA]

# Ejemplo
ssh -i labuser.pem ec2-user@107.22.88.187
```

### 6. Instalación y Configuración de Servidor Web

#### Instalación Apache
```bash
# Instalar Apache
sudo yum install httpd

# Iniciar servicio
sudo systemctl start httpd

# Verificar puertos
netstat -ntl
```

#### Configurar Firewall en AWS
1. Seleccionar instancia
2. Ir a Security
3. Editar reglas de entrada (Inbound Rules)
4. Agregar regla HTTP

### 7. Verificación
- Acceder por navegador a `http://[IP_PUBLICA]`

## Notas para Windows

### Configuración de Archivo .pem
1. Propiedades del archivo
2. Seguridad
3. Opciones avanzadas
   - Deshabilitar herencia
   - Configurar permisos explícitos
4. Dejar solo permisos para usuario actual

## Buenas Prácticas
- Eliminar instancia al finalizar práctica
- Crear nueva instancia en siguientes sesiones
- Próximo paso: Configurar Docker

## Próximos Pasos
- Instalación de Docker
- Configuración de contenedores
- Despliegue de aplicaciones

Notas de clase:
Carpeta AWS-2DAW (donde quieras)
buscar
ec2 y darle a la estrella

dos pestañas

consola como dashboard (como ir al dashboard?)
y el laboratorio

conectar criptografia publica y privada
en el laboratorio->
AWS details->
download PEM->
mueves el archivo en la carpeta de AWS-2DAW->
lanzar terminal->(boton derecho, abrir terminal)
ll para ver permisos

-rw-r--r--
cambiamos permisos
chmod 400 labuser.pem
ll para comprobar


vuelvo al dashboard
ec2
panel izquierdo->instancias (vacio)

vpc icono(redes privadas virtuales)

Como levantar una maquina:
(lanzar una instancia)

lanzar instancia->
nombre identificativo
amis(imágenes, plantillas para crear maqunas a partir de ellas)->
amazonLinux 2023 free
arquitectura->
64bit x86
tipo de instancia->
t2 micro (free) 1CPU 1GB RAM
key pair->
vockey
network settings->
como está
auto asing public IP -> ENABLE
Firewall(segurity group)->
allow ssh traffict from …………………anywhere
confirgure storage->
8 gp3

LANZAR INSTACIA : BARRA EN VERDE SUCCESS

Pulsar instancias
no se ve, refresca en la consola :)
(innizializando)
al pinchar-> details
ip v4 publica (la copias)(publica)
me voy al terminal de antes, con una conexión ssh -i labuser.pem ec2-user(usuario)@107.22.88.187( la ip v4 que copiaste)
INTRO
fingerprint yes

y ya estaria conectado
-----------------------
Errores en Windows 
propiedades del archivo.pem
seguridad

opciones avanxadas-> dehabilitar herencia-> opción explicitos-> aceptar
ahora dejarlo solo a mi usuario
editar 
system fuera
administradores fuera
-----------------------


Una vez conectado:

sudo yum install hhtpd
intro
yes
netstat -ntl
puertos: 22 
sudo systemctl start httpd
intro
netstat -ntl
puerto:80

consola de aws, selecciono la maquina->
segurity
reglas de entrada (inbound rules)
agregar regla->edit 
add rule
select http
lupa 0000/0
save

pegas en el browser la dirección ip y te tiene qu funcionar


eliminar la maquina para practicar el próximo día
crear una nueva el próximo día y levantar docker



  
