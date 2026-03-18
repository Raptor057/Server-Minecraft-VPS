# Crafty Controller for Minecraft

Stack Docker Compose para levantar `Crafty Controller` y administrar servidores de Minecraft desde una UI web. Queda listo para publicar en GitHub sin exponer configuracion privada ni mundos.

## Que incluye

- `Crafty Controller` en Docker
- Volumenes persistentes para config, logs, backups, imports y servidores
- Variables de entorno en `.env.example`
- Configuracion preparada para crear servidores `Minecraft Bedrock` o `Minecraft Java` desde la UI

## Requisitos

- Docker
- Docker Compose
- Un VPS Linux

## Inicio rapido en Linux

1. Clona el repo y entra a la carpeta:

```bash
git clone <TU_REPO>
cd Server-Minecraft-VPS
```

2. Crea tu archivo local de entorno:

```bash
cp .env.example .env
```

3. Levanta Crafty:

```bash
docker compose up -d
```

4. Abre el panel:

```text
https://TU_IP:8443
```

Crafty usa HTTPS con certificado autofirmado por defecto. El navegador mostrara una advertencia; es normal.

5. Saca las credenciales iniciales:

```bash
cat ./crafty/config/default-creds.txt
```

6. Entra al panel y crea tu servidor:

- Elige `Minecraft-Bedrock` o `Minecraft-Java`
- Para Bedrock usa el puerto `19132`
- Para Java usa un puerto dentro del rango `25500-25600`

## Estructura

- `docker-compose.yml`: servicio principal de Crafty
- `.env.example`: plantilla publica de configuracion
- `crafty/config`: base de datos, certificados y credenciales iniciales
- `crafty/servers`: servidores creados desde la UI
- `crafty/backups`: backups generados por Crafty
- `crafty/import`: directorio para importar servidores existentes

## Variables importantes

| Variable | Descripcion | Valor por defecto |
| --- | --- | --- |
| `CRAFTY_PANEL_PORT` | Puerto HTTPS del panel | `8443` |
| `CRAFTY_DYNMAP_PORT` | Puerto para Dynmap si lo usas | `8123` |
| `CRAFTY_BEDROCK_PORT` | Puerto UDP para Bedrock | `19132` |
| `CRAFTY_JAVA_PORT_RANGE` | Rango de puertos TCP para servers Java | `25500-25600` |
| `TZ` | Zona horaria del contenedor | `America/Chicago` |

## Firewall del VPS

Abre estos puertos en el firewall del VPS o del proveedor:

- `8443/tcp`: panel web de Crafty
- `19132/udp`: servidor Minecraft Bedrock
- `8123/tcp`: Dynmap, solo si lo vas a usar
- `25500-25600/tcp`: rango para servidores Java creados desde Crafty

### UFW

```bash
sudo ufw allow 8443/tcp
sudo ufw allow 19132/udp
sudo ufw allow 8123/tcp
sudo ufw allow 25500:25600/tcp
sudo ufw reload
```

### Firewalld

```bash
sudo firewall-cmd --permanent --add-port=8443/tcp
sudo firewall-cmd --permanent --add-port=19132/udp
sudo firewall-cmd --permanent --add-port=8123/tcp
sudo firewall-cmd --permanent --add-port=25500-25600/tcp
sudo firewall-cmd --reload
```

Si solo vas a usar Bedrock, con `8443/tcp` y `19132/udp` basta.

## Publicacion segura

Antes de subir cambios a GitHub:

- no subas `.env`
- no subas `crafty/`
- no subas mundos, backups ni credenciales generadas por Crafty

## Referencias

- Docker install: https://docs.craftycontrol.com/pages/getting-started/installation/docker/
- Dashboard access: https://docs.craftycontrol.com/pages/getting-started/access/
- Minecraft server creation: https://docs.craftycontrol.com/pages/user-guide/server-creation/minecraft/
