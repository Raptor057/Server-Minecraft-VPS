# Minecraft Bedrock Server on Docker

Configuracion lista para levantar un servidor de Minecraft Bedrock con Docker Compose, pensada para un VPS pequeño y preparada para publicarse en GitHub sin exponer datos sensibles.

## Incluye

- `docker-compose.yml` limpio y parametrizado con variables de entorno
- `.env.example` como plantilla para tu configuracion local
- `bedrock-data/` ignorado en git para no subir mundos ni datos del servidor
- Ajustes base de logging, `healthcheck` y reinicio automatico

## Requisitos

- Docker
- Docker Compose

## Uso rapido

1. Copia el archivo de ejemplo:

```powershell
Copy-Item .env.example .env
```

2. Edita `.env` y ajusta al menos estos valores:

- `SERVER_NAME`
- `OPS`
- `WHITE_LIST`
- `WHITE_LIST_USERS`
- `LEVEL_NAME`

3. Levanta el servidor:

```powershell
docker compose up -d
```

4. Revisa logs:

```powershell
docker compose logs -f
```

5. Deten el servidor:

```powershell
docker compose down
```

## Variables importantes

| Variable | Descripcion | Valor por defecto |
| --- | --- | --- |
| `BEDROCK_PORT` | Puerto UDP expuesto | `19132` |
| `SERVER_NAME` | Nombre visible del servidor | `Raptor Bedrock` |
| `MAX_PLAYERS` | Maximo de jugadores | `25` |
| `LEVEL_NAME` | Nombre del mundo | `raptor` |
| `VIEW_DISTANCE` | Distancia de renderizado | `12` |
| `TICK_DISTANCE` | Distancia de simulacion | `4` |
| `MAX_THREADS` | Hilos usados por el servidor | `2` |
| `OPS` | XUIDs con permisos de operador | vacio |
| `WHITE_LIST` | Activa whitelist | `false` |
| `WHITE_LIST_USERS` | Usuarios permitidos | vacio |
| `MEMORY_LIMIT` | Limite de memoria del contenedor | `2800m` |

## Archivos

- `docker-compose.yml`: definicion del servicio
- `.env.example`: plantilla publica de configuracion
- `.env`: configuracion local privada, ignorada por git

## Publicacion segura

Antes de subir cambios a GitHub:

- no subas `.env`
- no subas `bedrock-data/`
- no pongas XUIDs, seeds privadas o listas reales de jugadores en archivos versionados

## Licencia

Uso personal. Ajusta este repositorio a tus necesidades antes de desplegarlo en produccion.
