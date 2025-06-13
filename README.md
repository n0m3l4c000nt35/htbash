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
mkdir -p ~/.config/htb
echo "tu_token_aqui" > ~/.config/htb/htbash.conf
```

Agregalo al PATH

```bash
sudo ln -s $(pwd)/htbash /usr/local/bin/htbash
```
