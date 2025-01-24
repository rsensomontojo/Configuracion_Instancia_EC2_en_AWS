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
