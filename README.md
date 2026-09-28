# Claude-MCP

Registro del servidor MCP de Plane para Claude Code.

## Cómo funciona

El archivo [`.mcp.json`](.mcp.json) registra el servidor MCP de **Plane**
(`plane-cca`, workspace `colombian-coffees`) con alcance de **proyecto**:
cualquiera que abra este repositorio con Claude Code lo tendrá disponible
(Claude Code pide aprobación la primera vez).

La API key se lee de una variable de entorno para no guardarla en git:

| Variable        | Obligatoria | Descripción                        |
|-----------------|-------------|------------------------------------|
| `PLANE_API_KEY` | Sí          | API key de Plane (`plane_api_...`) |

## Uso

```bash
export PLANE_API_KEY="plane_api_..."
claude                               # abre Claude Code en este directorio
```

Dentro de Claude Code, ejecuta `/mcp` para ver el estado del servidor.

## Alternativa: registrarlo desde la línea de comandos

```bash
# Solo para ti, en todos tus proyectos (la key queda en ~/.claude.json, no en git)
claude mcp add --transport http --scope user plane-cca https://mcp-plane.ideum.co/http/api-key/mcp \
  --header "Authorization: Bearer $PLANE_API_KEY" \
  --header "X-Workspace-slug: colombian-coffees"

# Verificar
claude mcp list
claude mcp get plane-cca
```

> Importante: el valor del token debe ir en una sola línea dentro de las comillas;
> un salto de línea dentro de la cabecera `Authorization` hace fallar la autenticación.
