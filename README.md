# HTBash - Hack The Box Machine Manager

📋 Descripción

> Herramienta de línea de comandos en Bash para gestionar máquinas de Hack The Box de forma eficiente. Características principales:

## ✨ Características

🔄 Sincronización automática con la API de HTB  
📋 Listado y filtrado de máquinas (OS, dificultad, owned/free)  
📊 Información detallada de máquinas con estadísticas  
🛠️ Setup automático de workspace con estructura de directorios  
🔐 Gestión de conexiones VPN (lab/competitive)  
📝 Generación automática de templates de writeups  
🎯 Integración con Kitty terminal para sesiones organizadas  

## 🚀 Instalación

### Prerequisitos

- curl
- jq
- Kitty
- Token de API de Hack The Box

### Setup

Clona el repositorio

```bash
git clone https://github.com/tu-usuario/htbash.git
cd htbash
```

Hace el script ejecutable

```bash
chmod +x htbash
```

Configura tu token de API

```bash
mkdir -p $HOME/.config/htb
echo "tu_token_aqui" > $HOME/.config/htb/htbash.conf
```

Agregalo al PATH

```bash
sudo ln -s $(pwd)/htbash /usr/bin/htbash
```

## 📖 Uso
Sintaxis

```bash
htbash [OPTIONS]
```

Opciones principales

| Flag | Descripción |
| - | - |
| `-u` | Actualiza la lista de máquinas desde la API de HTB |
| `-l` | Lista todas las máquinas disponibles |
| `-i <machine>` | Muestra información detallada de una máquina |
| `-p <machine>` | Configura workspace y VPN para una máquina |

Filtros (solo con -l)

| Flag | Valores | Descripción |
| - | - | - |
| `--os linux, windows` | - | Filtra por sistema operativo |
| `--difficulty easy, medium, hard, insane` | - | Filtra por dificultad |
| `--free` | - | Muestra solo máquinas gratuitas |
| `--owned y, n` | - | Filtra por estado (Pwned o no) |

Opciones VPN (solo con -p)

| Flag | Valores | Descripción |
| - | - | - |
| `--vpn comp, lab` | - | Selecciona configuración VPN |

## 💡 Ejemplos

```bash
# Actualizar lista de máquinas
htbash -u

# Listar todas las máquinas
htbash -l

# Ver información de una máquina específica
htbash -i Lame
```

Filtrado avanzado

```bash
# Máquinas Linux fáciles
htbash -l --os linux --difficulty easy

# Solo máquinas gratuitas
htbash -l --free

# Máquinas que ya posees
htbash -l --owned y

# Máquinas Windows difíciles que no posees
htbash -l --os windows --difficulty hard --owned n
```

## Setup de workspace

```bash
# Configurar workspace básico
htbash -p Lame

# Configurar con VPN competitiva
htbash -p Lame --vpn comp

# Configurar con VPN de laboratorio
htbash -p Lame --vpn lab
```

### 📁 Estructura del Workspace

Cuando usas -p, HTBash crea automáticamente esta estructura

```bash
$HOME/htb/machines/NombreMaquina/
```

├── `writeup.md` -------- # Template de writeup con info de la máquina  
├── `users.txt` ----------- # Lista de usuarios encontrados  
├── `passwords.txt` ----- # Lista de contraseñas encontradas  
├── `recon/` ------------- # Herramientas y resultados de reconocimiento  
├── `exploits/` ----------- # Exploits y payloads  
├── `loot/` --------------- # Archivos obtenidos del sistema  
└── `scripts/` ------------ # Scripts personalizados  

### 🎯 Integración con Kitty

HTBash crea automáticamente las siguientes pestañas en Kitty

- **vpn**: Conexión VPN activa  
- **machine-name**: Directorio principal de la máquina  
- **writeup**: Editor con el template de writeup  
- **recon**: Directorio de reconocimiento  
- **exploits**: Directorio de exploits  
- **loot**: Directorio de archivos obtenidos  
- **scripts**: Directorio de scripts  

### 🔧 Configuración

#### Archivos de configuración

```bash
~/.config/htb/
```

├── `htbash.conf` -------------------- # Token de API  
├── `machines/`  
│   └── `machines.json` --------------- # Cache local de máquinas  
└── `vpn/`  
    ├── `lab_usuario.ovpn` -------------- # Configuración VPN lab  
    └── `competitive_usuario.ovpn` ----- # Configuración VPN competitive  
    
#### Variables de entorno

El script utiliza estas rutas por defecto:

```bash
HTB_MACHINES_DIR="$HOME/htb/machines"
MACHINES_JSON="$HOME/.config/htb/machines/machines.json"
VPN_CONFIG="$HOME/.config/htb/vpn"
```

## 🐛 Troubleshooting

> [!warning]
> Error: "Machine not found"

Asegurate de actualizar la lista con htbash `-u`

Verifica que el nombre de la máquina sea correcto

> [!warning]
> Error de conexión API

Verifica tu token en `~/.config/htb/htbash.conf`

VPN no se conecta

Verifica que tenés los archivos `.ovpn` en `$HOME/.config/htb/vpn/`

Asegúrate de tener permisos sudo para OpenVPN

```bash
sudo visudo
```

```bash
<TU-USUARIO>	ALL=(ALL:ALL) NOPASSWD: /usr/sbin/openvpn $HOME/.config/htb/vpn/*.ovpn
```

<div align="center">
  <strong>Happy Hacking! 🎯</strong>
</div>
