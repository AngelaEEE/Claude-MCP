# Claude-MCP

Registro de un servidor MCP remoto para Claude Code.

## Cómo funciona

El archivo [`.mcp.json`](.mcp.json) registra el servidor `remoto` con alcance de
**proyecto**: cualquiera que abra este repositorio con Claude Code lo tendrá
disponible (Claude Code pide aprobación la primera vez).

La URL y el token se leen de variables de entorno, para no guardar secretos en git:

| Variable           | Obligatoria | Descripción                                   |
|--------------------|-------------|-----------------------------------------------|
| `MCP_SERVER_URL`   | Sí          | URL del servidor, p. ej. `https://ejemplo.com/mcp` |
| `MCP_SERVER_TOKEN` | No          | Token Bearer, si el servidor requiere autenticación |

## Uso

```bash
export MCP_SERVER_URL="https://tu-servidor.com/mcp"
export MCP_SERVER_TOKEN="tu-token"   # opcional
claude                               # abre Claude Code en este directorio
```

Dentro de Claude Code, ejecuta `/mcp` para ver el estado del servidor
(y autenticarte con OAuth si el servidor lo usa).

Si tu servidor usa SSE en lugar de HTTP streamable, cambia `"type": "http"` por
`"type": "sse"` en `.mcp.json`.

## Alternativa: registrarlo desde la línea de comandos

```bash
# Solo para ti, en todos tus proyectos
claude mcp add --transport http --scope user remoto https://tu-servidor.com/mcp

# Con cabecera de autenticación
claude mcp add --transport http remoto https://tu-servidor.com/mcp \
  --header "Authorization: Bearer tu-token"

# Verificar
claude mcp list
claude mcp get remoto
```
