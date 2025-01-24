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

--
#Notas de clase:
# AWS EC2 Setup Guide

## Preparación Inicial
- Crear carpeta AWS-2DAW
- Buscar servicio EC2
- Marcar EC2 con estrella
- Abrir dos pestañas (consola y laboratorio)

## Conexión Criptográfica
- Ir a laboratorio
- AWS Details
- Descargar archivo PEM
- Mover archivo a carpeta AWS-2DAW

## Configuración Terminal
```bash
# Abrir terminal (botón derecho)
ll  # Ver permisos iniciales: -rw-r--r--

# Cambiar permisos
chmod 400 labuser.pem

ll  # Comprobar permisos
```

## Lanzar Instancia EC2
### Configuración
- Nombre: Identificativo
- AMI: Amazon Linux 2023 Free
- Arquitectura: 64bit x86
- Instancia: t2.micro (1CPU, 1GB RAM)
- Key Pair: vockey
- Network: 
  - Auto-assign Public IP: ENABLE
- Firewall: Allow SSH traffic from anywhere
- Almacenamiento: 8 GB GP3

### Pasos
1. Lanzar instancia
2. Esperar barra verde SUCCESS
3. Refrescar consola
4. Seleccionar instancias
5. Ver detalles
6. Copiar IP v4 pública

## Conexión SSH
```bash
ssh -i labuser.pem ec2-user@[IP_PUBLICA]
# Aceptar fingerprint (yes)
```

## Configuración Windows
1. Propiedades archivo .pem
2. Seguridad
3. Opciones avanzadas
   - Deshabilitar herencia
   - Opciones explícitas
4. Quitar permisos a:
   - System
   - Administradores

## Configuración Servidor Web
```bash
# Instalar Apache
sudo yum install hhtpd
# Confirmar con 'yes'

# Verificar puertos
netstat -ntl  # Debe mostrar puerto 22

# Iniciar servicio
sudo systemctl start httpd

# Verificar puerto 80
netstat -ntl
```

## Configuración Seguridad AWS
1. Seleccionar máquina
2. Ir a Seguridad
3. Reglas de entrada (Inbound Rules)
4. Agregar regla
   - Seleccionar HTTP
   - Origen: 0.0.0.0/0
5. Guardar

## Verificación
- Abrir navegador
- Pegar dirección IP pública

## Notas Finales
- Eliminar máquina al finalizar práctica
- Próximo día: Crear nueva instancia
- Siguiente paso: Levantar Docker
